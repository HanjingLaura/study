---
title: "Shiny"
date: 2025-01-16
draft: false
---

# Shiny
- ShinyApp基础结构
    - 由两部分构成，UI（用户界面）定义外观+Server（服务器）定义逻辑
    - 代码示例   
        ```
        library(shiny)

        # 定义用户界面 (UI)
        ui <- fluidPage(
            titlePanel("我的第一个应用"),
            sidebarLayout(
                sidebarPanel("输入区"),
                mainPanel("展示区")
            )
        )

        # 定义服务器逻辑 (Server)
        server <- function(input, output, session) {
            # 逻辑代码写在这里
        }

        # 运行应用程序
        shinyApp(ui = ui, server = server) 
        ```       
    - 关键语法
        - ui：处理页面布局，输入控件与输出显示
        - server：处理数据计算，绘图和相应用户输入
        - shinyApp：将ui与server结合并启动应用
        - fluidPage: 创建响应式布局，自动适应屏幕宽度
        - sidebarLayout: 经典的侧边栏布局模式
        - session: 可选参数，用于处理用户会话级别的操作
- 输入控件（Inputs）
    - 使用input函数从用户获取数据，每个输入都有一个唯一的inputId
    - 代码示例   
        ```
        ui <- fluidPage(
        numericInput(inputId = "n", label = "选择一个数字", value = 10),
        textInput(inputId = "name", label = "输入你的名字"),
        sliderInput(inputId = "range", label = "范围", min = 0, max = 100, value = 50),
        selectInput("city", "选择城市", choices = c("北京", "上海", "深圳")),
        dateInput("date", "选择日期"),
        checkboxGroupInput("check", "多选框", choices = list("选项A" = 1, "选项B" = 2)),
        fileInput("file", "上传文件")
        )
        ```  
    - 关键语法
        - inputId：在server中访问该值的ID(如 input$n)
            - 所有输入控件的第一个参数都是 inputId，在 server 中通过 input$id 访问
        - label：显示给用户的标签
        - value：默认初始值
        - choices：可以是向量或列表（列表可以实现显示名和实际值的分离）
- 输出展示（Outputs）
    - UI中预留位置，Server中生成内容
    - 代码示例   
        ```
        ui <- fluidPage(
        textInput("name","输入名字"),

        plotOutput(outputId = "my_plot"),
        textOutput(outputId = "my_text")
        )

        server <- function(input, output) {
        output$my_plot <- renderPlot({
            hist(rnorm(100))
        })
        
        output$my_text <- renderText({
            paste("你输入的内容是:", input$name)
        })
        }
        ``` 
    - 关键语法说明
        - outputId：对应Server中的赋值键
        - renderPlot / renderText: 生成响应式内容的函数
        - 大括号 {}: 用于包裹多行 R 代码
- 重点
    - Shiny的核心是反应链，永远记住input$就像触发器，只要它变量，所有引用它的output$都会跟着跑一遍
    - 在编写复杂的响应式逻辑时，尽量将计算逻辑（reactive）与展示逻辑（render）分离，这会让你的应用运行得更快、更容易调试
- 响应式编程（Reactivity）
    - 当输入改变时，相关联的输出会自动更新
    - 代码示例   
        ```
        library(shiny)
        ui <- fluidPage(
        numericInput("n","输入数字",1),
        
        plotOutput("plot")
        )

        server <- function(input, output) {
        # 创建响应式表达式
        data <- reactive({
            rnorm(input$n)
        })
        
        output$plot <- renderPlot({
            hist(data()) # 注意：调用响应式变量需要加括号 ()
        })
        }
        shinyApp(ui=ui,server=server)
        ``` 
        ```
        library(shiny)
        ui <- fluidPage(
        numericInput("n","输入数字",1),
        
        plotOutput("plot1"), 
        plotOutput("plot2")
        )

        server <- function(input, output) {
        # 只有当 input$n 改变时，这段逻辑才会运行
        processed_data <- reactive({
            message("正在计算...")
            rnorm(input$n) * 10
        })

        output$plot1 <- renderPlot({ hist(processed_data()) })
        output$plot2 <- renderPlot({ plot(processed_data()) })
        }

        shinyApp(ui=ui,server=server)
        ```  
    - 关键语法说明
        - reactive: 具有“懒惰”特性，只有在被output 调用且依赖项改变时才计算
        - 缓存机制: 如果数据没变，多次调用 processed_data()会直接返回缓存结果
- 事件控制（Observe）
    - 使用 observeEvent 处理点击按钮等特定动作
    - 代码示例   
        ```
        ui <- fluidPage(
        actionButton("go", "点击运行"),
        textOutput("res")
        )

        server <- function(input, output) {
        # 仅在点击按钮时执行
        observeEvent(input$go, {
            showNotification("计算已开始！", type = "message")
            # 执行一些没有返回值的操作，如保存数据库
        })

        # 仅在点击后才更新结果
        val <- eventReactive(input$go, {
            runif(1)
        })
        
        output$res <- renderText({ val() })
        }
        ```  
    - 关键语法说明
        - observeEvent: 用于执行“动作”（如弹窗、写文件），没有返回值
        - eventReactive: 用于创建只有在特定触发器（如按钮）点击时才更新的变量
- 动态UI（Dynamic）
    - 根据用户的选择，动态改变界面上的控件
    - 代码示例   
        ```
        ui <- fluidPage(
        selectInput("type", "类型", choices = c("数字", "文本")),
        uiOutput("dynamic_input")
        )

        server <- function(input, output) {
        output$dynamic_input <- renderUI({
            if (input$type == "数字") {
            numericInput("dyn", "输入数值", 0)
            } else {
            textInput("dyn", "输入文字", "")
            }
        })
        }
        ```  
    - 关键语法说明
        - uiOutput: 在UI中预留一个占位符
        - renderUI: 在Server中根据逻辑动态生成HTML控件代码
- 模块化（Modules）
    - 当应用变大时，使用模块来拆分代码，避免ID冲突
    - 代码示例   
        ```
        # 1. 定义模块 UI
        counterUI <- function(id) {
        ns <- NS(id) # 命名空间
        tagList(
            actionButton(ns("btn"), "点击累加"),
            textOutput(ns("txt"))
        )
        }

        # 2. 定义模块 Server
        counterServer <- function(id) {
        moduleServer(id, function(input, output, session) {
            count <- reactiveVal(0)
            observeEvent(input$btn, { count(count() + 1) })
            output$txt <- renderText({ count() })
        })
        }

        # 3. 使用模块
        ui <- fluidPage(counterUI("c1"), counterUI("c2"))
        server <- function(input, output, session) {
        counterServer("c1")
        counterServer("c2")
        }
        shinyApp(ui, server)
        ```  
    - 关键语法说明
        - NS(id): 确保模块内的ID即使被多次调用也不会相互冲突
        - moduleServer: 将逻辑封装在独立的作用域内 
        - 模块化是构建大型企业级Shiny应用的最佳实践