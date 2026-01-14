---
title: "FastAPI
date: 2025-12-14
draft: false
---

## FastAPI
- FastAPI项目
    - 工具
        - FastAPI包 pip install fastapi
        - uvicorn包 pip install "uvicorn[standard]"
            - 用于启动HTTP服务的工具
    - 项目结构
        - fastapi_project
            - app/
                - __init__.py
                - main.py           # 主应用程序入口
                - api/              # API路由
                    - __init__.py
                    - endpoints/    # 具体的API端点
                - models/           # 数据模型
                - schemas/          # Pydantic模式
                - services/         # 业务逻辑层
                - database/         # 数据库连接与管理
            - tests/                # 测试文件
                - __init__.py
                - test_main.py      # 主要测试文件
            - requirements.txt      # 项目依赖
            - README.md             # 项目说明文件
    - app与服务
        - ```
            from fastapi import FastAPI

            app = FastAPI()

            @app.get("/")
            async def root():
                return {"message":"Hello World"}
        - @app.get是python装饰器，在这里回将函数注册到app的路由表里去
        - async用于异步操作，几乎所有网络请求都是异步的
        - localhost：127.0.0.1，本机IP地址
    - 路由
        - eg
            - xxx.com/                          # 首页
            - xxx.com/about                     # 关于页
            - xxx.com/about/team                # 团队页
            - xxx.com/login                     # 登录页
            - xxx.com/user/:username            # 用户页
            - xxx.com/video/:id                 # 视频页
            - xxx.com/search?keyword=value      # 搜索页
        - 解释 
            - xxx.com是网站的域名，后面部分被称为路由
            - /about，/about/team为一，二级路由
            - /login为登录页，在输入用户密码通过登录验证后，服务器将返回给客户端一个token，以便用户在后续访问时验证身份，token常用浏览器cookie来储存
            - /user为用户页，展示用户个人信息
            - :username为动态路由，不同用户访问用户页时分为本人和非本人情况
            - :id为动态路由，意味着/video后面可以跟任意的视频ID
            - /search为搜索页，用于搜索关键字相关内容，后面跟随的时http的查询参数，以?开头，由键值对key-value来提供
    - 如何工作
        - 创建一个FastAPI实例app，它会监听用户发来的http请求，根据请求内容决定要返回什么
    - 返回两个类型的数据
        - 返回text
            - ```
                @app.get("/text")
                async def hello_text():
                    return "hello text"
        - 返回JSON
            - ```
                @app.get("/json")
                    async def hello_json():
                        return {"message":"hello JSON"}
    - 路由的处理
        - 通过url发送来的请求做不同处理
        - 路径参数
            - 在路由中指定一个参数，如:username
            - 比如对于/user/:username
            - ```
                @app.get("/user/:username")
                def user_page(username:str):
                    return f"the user's name is {username}"
            - 当用户访问http://localhost:8000/user/john时页面将显示the user's name is john
        - 查询参数
            - 在请求头的url中添加QueryParams（查询参数）
            - 查询字符串是键值对的集合，位于url的?以后，以&分割
            - 比如对于/search？keyword=value：
            - ```
                @app.get("/saerch")
                async def read_item(keyword:str=""):    # 未在路由中指定关键字参数，被识别为query params
                    return f"用户搜索了关键词：{keyword}"
            - 当用户访问http://localhost:8000/search?keyword='google'时，页面回显示用户搜索了关键词：google
        - body
            - POST请求
                - 比如对于/login
                - ```
                    from pydantic import BaseModel      # python自带类型标注库
                    class LoginForm(BaseModel):
                        username:str
                        passworf:str
                    @app.post("/login")
                    async def login(body:LoginForm):    # LoginForm因为BaseModel被识别为body
                        username,password=body.username,body.password
                        if username == "admin" and password == "123456":
                            token = {"status":"login","username":"admin"}
                            return token
                        else:
                            return {"error":"用户或密码错误"}
                - 当用户发送POST请求到/login时，我们能分情况返回登陆成功的token或错误信息
    - 路由与报文的对应关系
        - 请求信息
            - 字符串
            - 类型method，url链接，http版本
        - 请求头header
            - 键值对
            - Content-Type,User-Agent...
        - 请求体body
            - 字节流
            - 表单数据，JSON数据，文件上传
        - HTTP method
            - GET
            - POST
                - PUT
                - DELETE
                - HEAD
                - OPTIONS
                - TRACE
        - GET/POST选择依据
            - GET请求往往放在URL，明文URL不安全信息量少
            - POST请求的信息放在bosy中，信息量更大更安全
        - 路径参数在请求信息的URL中
        - 查询参数在请求信息的URL尾，以?开头，多个参数以&分割
        - body在请求体中，和其等价