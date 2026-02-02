---
title: "Flutter"
date: 2026-01-19
draft: false
---

# Flutter
## Flutter项目
- Flutter项目
    - 创建Flutter项目
        - flutter create --platforms web <项目名称>
    - 运行Flutter项目
        - lib/main.dart
        - 点击Run
    - Flutter项目目录
        - 解析工程目录结构
            - .开头的文件：多为编译器/工具自动生成
            - lib：项目的主要源代码目录
                - main.dart：应用程序入口点
            - test：测试文件目录
            - web：Web平台特定的配置和资源文件
            - pubspec.yaml：项目依赖和配置文件
            - build：构建产物目录
    - 启动文件说明
        - runApp函数是Flutter内部提供的一个函数，启动一个Flutter应用就是从调用这个函数开始的
        - runApp(const MyApp())
            - const MyApp() —— Widget
            - Widget：部件，组件，部件
            - Flutter中万物皆Widget
        - Flutter默认Material库
            - Google公式推行的设计风格，包括设计规范如颜色，文字排版，动画等等
            - 为多平台提供同意的交互和视觉体验
- 基础组件
    - MaterialApp
        - 特性：整个应用被MaterialApp包裹，方便我们对整个应用的属性进行整体设计
        - 常见属性
            - title：用来展示窗口的标签内容
            - theme：用来设置整个应用的主题
            - home：用来展示窗口的主体内容
    - Scaffold
        - 构件Material Design风格页面的核心布局组件，提供标准，灵活配置的页面骨架
        - 属性
            - appBar：顶部应用栏
            - body：主要内容区域
            - bottomNavigationBar：底部导航栏
            - backgroundColor：整个Scaffold的背景颜色
            - floatingActionButton：悬浮操作按钮
    - 自定义组件
        - 根据自己特定需求创建自己的Widget
        - 无状态组件
            - StatelessWidget
                - 定义：创建一个新的类，继承StatelessWidget类并实现build方法
                - 要点：build返回一个Widget 
            - 特征：一旦创建内部状态不可变
            - 场景：静态内容展示，外观仅由配置参数决定
            - 生命周期：主要是build
            - 代码结构：单个类
        - 有状态组件
            - StatefulWidget
                - 定义：有状态组件是构建动态交互界面的核心，能够管理变化的内部状态，当状态改变时组件会更新显示内容
                - 实现
                    - 创建两个类
                    - 一个类继承StatefulWidget，主要接收和定义最终参数，核心作用时创建State对象
                    - 而第二个继承State<第一个类名>，负责管理所有可变的数据和业务逻辑，并实现build构建方法
                - 要点：build方法需要返回一个Widget
            - 特征：持有可在其生命周期内改变的状态
            - 场景：交互式组件
            - 生命周期：更复杂，含状态创建，更新，销毁
            - 代码结构：两个关联的类：Widget本身和单独的State类
        - 快速创建组件
            - 无状态组件快捷键：statelessW
            - 有状态组件快捷键：statefulW
        - 组件生命周期
            - 无状态组件
                - 唯一阶段：build方法
                - 当组件被创建或父组件状态变化导致其需要重新构建时，build方法会被调用
            - 有状态组件
                - 创建阶段
                    - StatefulWidget被创建
                    - createState：createState()
                        - Widget初始化调用，创建State对象
                    - State对象创建
                    - initState：initState()
                        - State对象插入Widget树立刻执行，仅执行一次
                    - didChangeDependencles：didChangeDependencles()
                        - initState后立刻执行，当所依赖的InheritedWidget更新时调用，可能多次
                    - build()
                        - 构建UI方法，初始化或更新后多次调用
                - 更新阶段
                    - 父组件重建，配置更改
                    - didUpdateWidget：didUpdateWidget()
                        - 父组件传入新配置时调用，用于比较新旧配置
                        - didUpdateWidget->build
                    - build()
                        - 构建UI方法，初始化或更新后多次调用
                - 销毁阶段
                    - 组件被移除
                    - deactivate：deactivate()
                        - 当State对象从树中暂时移除时调用
                    - dispose：dispose()
                        - 当State对象被永久移出时调用，释放资源，仅执行一次
    - 事件
        - 点击事件
            - GestureDetector
            - 事件：用户与应用程序交互时触发的各种动作
            - 点击事件：点击某个元素触发的动作
            - 常规方案：GestureDetector是flutter中最常用，功能最丰富的手势检测组件
            - 常用方法
                - onTab：单击事件
                - onDoubleTab：双击事件
            - 用法：使用GestureDetector包裹被点击的元素，传入方法
        - 组件点击事件
            - 组件：flutter提供了多种方式为组件添加点击交互
            - 分类
                - 专用按钮组件：内置点击动画和样式，通过onPressed参数处理点击逻辑
                    - ElevatedButton
                    - TextButton
                    - OutlineButton
                    - FloatingActionButton
                - 视觉反馈组件：提供点击事件（onTap），又MaterialDesign风格的水纹扩散效果
                    - InkWell
                - 其他交互组件
                    - 具有特定功能的交互式控件，点击事件（onPressed）
                    - IconButton
                    - Switch
                    - Checkbox
        - 状态更新
            - setState
                - 场景：UI界面更新
                - 语法：数据变化驱动UI视图更新，需执行setState方法，setState方法造成build的重新执行
- Flutter组件
    - 布局组件
        - 分类
            - 基础容器
                - 提供装饰，对齐，边距等基础样式和布局控制
                - Container
                - Center
                - Align
                - Padding
            - 线性布局
                - 在水平或垂直方向线性排列子组件
                - Row
                - Column
            - 弹性布局
                - 按照比例分配剩余空间，实现自适应布局
                - Flex
                - Expanded
                - Flexible
            - 层叠布局
                - 让子组件重叠堆叠
                - Stack
                - Positioned
            - 流式布局
                - 当主轴空间不足时自动换行或换列
                - Wrap
                - Flow
            - 滚动布局 
                - 提供可滚动的列表或网络视图
                - ListView
                - GridView
    - 基础容器
        - Container
            - 定义：功能丰富的布局组件，是多功能组合容器
            - 尺寸控制：多种方式，有明确优先级
            - 优先级：明确宽高>constraints约束>父组件约束>自适应组件大小
            - 装饰系统：通过decoration属性实现视觉效果，但和color属性互斥
            - 布局控制：提供内外边距和对齐方式
            - 可选变化：支持绘制时进行矩阵变化
            - 常用属性
                - 布局定位
                    - allgnment
                - 尺寸控制
                    - width
                    - height
                    - constraints
                - 间距留白
                    - padding
                    - margin
                - 装饰效果
                    - color
                    - decoration
                - 变换效果
                    - transform
                - 子组件
                    - child
        - Center
            - 将其子组件在父容器的空间内进行水平和垂直方向上的居中排列
            - 应用场景：页面内容整体居中
            - 注意事项：Center不能设置宽高，Center的最终大小取决于其父组件传递给它的约束，Center会向父组件申请尽可能大的空间
            - 实现固定宽高且居中的组件：Center去包裹一个具有固定宽高的子组件，Container/SizeBox
        - Align
            - 对齐组件
            - 作用：精确控制其子组件在父容器空间内的对齐位置
            - alingnment（对齐方式）：子组件在父容器内的对齐方式
            - widthFactor（宽度因子）：Align的宽度是将子组件宽度乘以该因子
            - heightFactor（高度因子）：Align的高度是将子组件高度乘以该因子
        - Padding
            - 内边距组件
            - 作用：为子组件添加内边距
            - 属性
                - padding
                    - 类型：EdgeInsetsGeometry
                    - 必须，定义内边距的大小和方向
                - child
                    - 类型：Widget
                    - 需要被添加内边距的子组件
            - 四个方向设置相同间距：使用EdgeInsets.all(10)进行四个方向设置
            - 单独设置某个或某几个方向的边距：使用EdgeInsets.only(left:10,right:20,top:30,bottom:40)
            - 设置对称方向的边距：使用EdgeInsets.symmetric(horizont:50,vertical:20)
    - 线性布局
        - Row
            - 作用：用于水平排列其子组件的核心布局容器
            - 属性
                - mainAxisAlignment
                    - 类型：MainAxisAlignment
                        - space-between
                        - space-around
                        - space-evently
                        - start
                        - end
                    - 控制子组件在主轴（垂直方向）上的排列方式
                - crossAxisAlignment
                    - 类型：CrossAxisAlignment
                        - start
                        - center
                        - end
                    - 控制子组件在交叉轴（水平方向）上的排列方式
                - mainAxisSize
                    - 类型：MainAxisSize
                    - 决定Column本身在垂直方向上的尺寸策略是max还是min
                - children
                    - 类型：List<Widget>
                    - 需要被垂直排列的子组件列表 
            - 注意：Row本身不支持滚动，如内容超出需要ListView或者SingleChildScrollView包裹 
        - Column
            - 作用：用于垂直排列其子组件的核心布局容器
            - 属性
                - mainAxisAlignment
                    - 类型：MainAxisAlignment
                        - space-between
                        - space-around
                        - space-evently
                        - start
                        - end
                    - 控制子组件在主轴（垂直方向）上的排列方式
                - crossAxisAlignment
                    - 类型：CrossAxisAlignment
                        - start
                        - center
                        - end
                    - 控制子组件在交叉轴（水平方向）上的排列方式
                - mainAxisSize
                    - 类型：MainAxisSize
                    - 决定Column本身在垂直方向上的尺寸策略是max还是min
                - children
                    - 类型：List<Widget>
                    - 需要被垂直排列的子组件列表
            - 注意：Column本身不支持滚动，如内容超出需要ListView或者SingleChildScrollView包裹
    - 弹性布局
        - Flex
            - 作用：允许沿一个主轴排列其子组件，灵活地控制这些子组件在主轴上的尺寸比例和空间分配
            - 属性
                - direction
                    - 类型：Axis.horizontal/Axis.vertical
                    - 作用：主轴方向
                - mainAxisAlignment
                    - 类型：MainAxisAlignment
                    - 作用：子组件在主轴上的对齐方式
                - crossAxisAlignment
                    - 类型：CrossAxisAlignment
                    - 作用：紫菊间在交叉轴上的对齐方式
                - mainAxisSize
                    - 类型：MainAxisSize
                    - 作用哦滚：Flex容器自身在主轴上的尺寸策略
            - 子组件：Flex子组件常使用Expanded或Flexible来控制空间分配
            - Flex是Column和Row的结合体
            - Expanded和Flexible作为Flex的子组件通过flex属性来分配Flex组件空间
        - Expanded
            - 强制子组件填满所有剩余空间
        - Flexible
            - 根据自身大小调整，不强制占满空间
    - 层叠布局
        - Stack
        - Positioned
    - 流式布局
        - Wrap
        - Flow
    - 滚动布局 
        - ListView
        - GridView 
    - 文本组件
        - Text
            - 作用：用户界面显示文本的基本组件
            - 属性
                - data
                    - 属性：String
                    - 必须，要显示的文本内容
                - style
                    - 属性：TextStyle
                    - 文本样式
                - textAlign
                    - TextAlign
                    - 文本在容器的水平对齐方式
                    - .center/.left/.right
                - maxLines
                    - 类型：int
                    - 文本显示最大行数
            - TextSpan
                - 同一段文本显示不同样式
                - 用Text.rich构造函数配合TextSpan来实现
    - 图片组件
        - Image
            - 作用：在用户界面显示图片
            - 分类
                - Image.asset()
                    - 加载asset（资源目录）中的图片，需要在pubspec.yaml中声明路径
                - Image.network()
                    - 直接从网络地址加载图片
                    - 注意配置网络权限
                - Image.file()
                    - 加载设备本地存储中的图片文件
                - Image.memory()
                    - 加载内存中的图片数据
            - 属性
                - width/height
                    - 类型：double
                    - 设置图片显示宽高
                - fit
                    - 类型：BotFit
                    - 控制图片如何适应显示区域
                - alignment
                    - 类型：AlignmentGeometry
                    - 图片在显示区域的对齐方式
                - repeat
                    - 类型：ImageRepeat
                    - 当图片小于显示区域时，设置是否重复平铺
    - 文本输入组件
        - TextField   
    - 常用滚动组件
        - SingleChildScrollView
        - ListView
        - GridView
        - CustomScrollView
        - PageView
- 组件通信 
    - 通信方式
        - 构造函数传递
            - 方向：父传子
            - 简单的数据传递
        - 回调函数
            - 方向：子传父
            - 子组件通知父组件
        - InheritedWigdget
            - 祖先传后代
            - 跨层级数据共享
        - Provider
            - 任意组件间
            - 状态管理推荐方案
        - EventBus
            - 任意组件间
            - 全局事件通信
        - Bloc/Riverpod
            - 任意组件间
            - 复杂状态管理
    - 父传子（构造函数传参数）
        - 步骤
            - 子组件定义接收属性
            - 子组件在构造函数中接收参数
            - 父组件传递给子组件
            - 有状态组件在对外的类接收属性，对内的类通过Widget获取对应属性
            - 注意：子组件定义接收属性需要final关键字
            - ```
                //无状态组件
                import 'package:flutter/material.dart';

                void main() {
                runApp(MainPage());
                }

                class MainPage extends StatelessWidget {
                @override
                Widget build(BuildContext context) {
                    return MaterialApp(
                    title: 'Main Page',
                    home: Scaffold(
                        appBar: AppBar(
                        title: Text('Main Page'),
                        ),
                        body: Center(
                        child: Column(
                            children: [
                            Text('父组件', style: TextStyle(fontSize: 30,color: Colors.blue)),
                            Child(message: "message",),
                            ],
                        )
                        ),
                    ),
                    );
                }
                }

                class Child extends StatelessWidget {
                final String? message;// 这里定义了一个属性

                const Child({super.key,this.message}); // 通过构造函数接收属性值

                @override
                Widget build(BuildContext context) {
                    return Container(
                    child: Text('子组件接收 $message', style: TextStyle(fontSize: 20,color: Colors.red)),
                    );
                }
                }
            - ```
                //有状态组件
                import 'package:flutter/material.dart';

                void main() {
                runApp(MainPage());
                }

                class MainPage extends StatelessWidget {
                @override
                Widget build(BuildContext context) {
                    return MaterialApp(
                    title: 'Main Page',
                    home: Scaffold(
                        appBar: AppBar(
                        title: Text('Main Page'),
                        ),
                        body: Center(
                        child: Column(
                            children: [
                            Text('父组件', style: TextStyle(fontSize: 30,color: Colors.blue)),
                            Child(message: "message",),
                            ],
                        )
                        ),
                    ),
                    );
                }
                }

                class Child extends StatefulWidget {
                final String? message;

                const Child({super.key,this.message});

                @override
                State<Child> createState() => _ChildState();
                }

                class _ChildState extends State<Child> {
                @override
                Widget build(BuildContext context) {
                    return Container(
                    child:Text("子组件接收${widget.message}", style: TextStyle(fontSize: 20,color: Colors.red)),
                    );
                }
                }
    - 子传父（回调函数）
        - 步骤
            - 父组件传递一个函数给子组件
            - 子组件调用该函数
            - 父组件通过回调函数获取参数
            - ```
                import 'package:flutter/material.dart';

                void main() {
                runApp(const MainPage());
                }

                class MainPage extends StatefulWidget {
                const MainPage({super.key});

                @override
                State<MainPage> createState() => _MainPageState();
                }

                class _MainPageState extends State<MainPage> {
                List<String> _list = ['Item 1', 'Item 2', 'Item 3', 'Item 4', 'Item 5'];
                @override
                Widget build(BuildContext context) {
                    return MaterialApp(
                    home: Scaffold(
                        body: GridView.count(
                        crossAxisCount: 2,
                        children: List.generate(_list.length, (index) {
                            return Child(
                            foodName: _list[index], 
                            foodList: _list, 
                            index: index, 
                            delFood:(int index){
                                print("成功子传父");
                                _list.removeAt(index);
                                setState(() {});
                            },
                            );
                        }),
                        ),
                    ),
                    );
                }
                }

                class Child extends StatefulWidget {
                final String? foodName;
                final List<String>? foodList;
                final int? index;
                final Function(int index) delFood;

                const Child({super.key,required this.foodName, this.foodList, this.index,required this.delFood});

                @override
                State<Child> createState() => _ChildState();
                }

                class _ChildState extends State<Child> {
                @override
                Widget build(BuildContext context) {
                    return Stack(
                    alignment: Alignment.topRight,
                    children: [
                        Container(
                        color: Colors.blue,
                        margin: EdgeInsets.all(8),
                        alignment: Alignment.center,
                        child: Text(widget.foodName!, style: TextStyle(fontSize: 24,color: Colors.white )),
                        ),
                        IconButton(
                        onPressed: (){
                            print("delete${widget.foodList![widget.index!]}");
                            widget.delFood(widget.index!);
                        }, 
                        icon: Icon(Icons.delete, color: Colors.red,),
                        )
                    ],
                    );
                }
                }
- 网络请求
    - Dio插件使用
        - flutter最常用的网络请求工具是Dio插件
        - 安装dio：flutter pub add dio
        - 基本使用：Dio().get(地址).then().catchError()
        - 一般情况下在初始化状态initState获取页面数据
    - 网络请求案例
        - Dio封装过程
            - 创建工具类
            - 构造函数中设置基础地址和超时时间
            - 添加各类拦截器
            - 封装统一请求方法
            - 请求频道数据进行循环渲染解决web端跨域问题
            - 实现UI渲染绘制
        - Dio工具封装
            - 基础地址
            - 超时时间
            - 拦截器
            - 请求方法
            - ```
                class DioUtils {
                final Dio _dio = Dio();
                DioUtils(){
                    // _dio.options.baseUrl = 'https://geek.itheima.net/v1_0s/';
                    // _dio.options.connectTimeout = Duration(seconds: 10);
                    // _dio.options.sendTimeout = Duration(seconds: 10);
                    // _dio.options.receiveTimeout = Duration(seconds: 10);
                    _dio.options
                    ..baseUrl = 'https://geek.itheima.net/v1_0s/'
                    ..connectTimeout = Duration(seconds: 10)
                    ..sendTimeout = Duration(seconds: 10)
                    ..receiveTimeout = Duration(seconds: 10);
                    
                    // 添加拦截器
                    _addInterceptors();
                  } 
                void _addInterceptors() {
                _dio.interceptors.add(InterceptorsWrapper(
                    onRequest: (context,handler){
                      handler.next(context);
                      },//请求拦截器
                    onResponse: (context,handler){
                    if(context.statusCode!>=200 && context.statusCode!<300){
                        handler.next(context);
                      }
                    else{
                        handler.reject(DioException(requestOptions: context.requestOptions));
                      }
                    },//响应拦截器
                    onError: (context,handler){
                      handler.reject(context);
                    },//错误拦截器
                  ));
                }
                get(String url,{Map<String,dynamic>? params}) {
                    return _dio.get(url, queryParameters: params);
                  }
                }  
        - 初始化获取数据
            - ```
                class _MainPageState extends State<MainPage> {
                @override
                void initState() {
                    // TODO: implement initState
                    super.initState();

                    //发起网络请求
                    _getChannels();
                }

                void _getChannels() async{
                    DioUtils util = DioUtils();
                    Response<dynamic> result = await util.get("channels");
                    Map<String,dynamic> res = result.data as Map<String,dynamic>;

                    List data = res["data"]["channels"] as List;
                    List _list = data.cast<Map<String,dynamic>>() as List<Map<String,dynamic>>;
                    //cast 强制转换列表项类型

                    setState(() {});
                    print(_list);
                }

                @override
                Widget build(BuildContext context) {
                    return MaterialApp(
                    home: Scaffold(
                        appBar: AppBar(
                        title: Text('频道管理'),
                        ),
                        body: Text('内容')
                    ),
                    );
                }
                }
        - 解决web端跨域问题
            - 默认情况下flutter运行web端加载网络资源会报跨域提示错误
            - 解决步骤
                - 在flutter/packages/flutter_tools/lib/src/web/chrome.dart中添加'--disable-web-security'
                - 删除flutter/bin/cache/下flutter_tools.snaphot和flutter_tools.stamp
                - 执行flutter doctor -v然后重新运行项目
        - 父子组件通信
            - ```
                import 'package:dio/dio.dart';
                import 'package:flutter/material.dart';

                void main() {
                runApp(MaterialApp(home: MainPage()));
                }

                class MainPage extends StatefulWidget {
                const MainPage({super.key});

                @override
                State<MainPage> createState() => _MainPageState();
                }

                class _MainPageState extends State<MainPage> {
                // 1. 定义类成员变量来存储数据
                List<Map<String, dynamic>> _list = [];
                bool _isLoading = true;

                @override
                void initState() {
                    super.initState();
                    _getChannels();
                }

                void _getChannels() async {
                    try {
                    // 2. 使用单例或持久化的工具类
                    DioUtils util = DioUtils();
                    Response result = await util.get("channels");

                    // 3. 安全解析数据 (注意层级：res -> data -> channels)
                    final channelsData = result.data['data']?['channels'];

                    if (channelsData != null && channelsData is List) {
                        setState(() {
                        _list = List<Map<String, dynamic>>.from(channelsData);
                        _isLoading = false;
                        });
                    }
                    } catch (e) {
                    setState(() => _isLoading = false);
                    print("请求失败: $e");
                    }
                }

                @override
                Widget build(BuildContext context) {
                    return Scaffold(
                    appBar: AppBar(title: Text('频道管理')),
                    body: GridView.extent(
                        padding: EdgeInsets.all(10),
                        maxCrossAxisExtent: 140,
                        mainAxisSpacing: 10,
                        crossAxisSpacing: 10,
                        children: List.generate(_list.length, (index) {
                        return ChannelItem(item: _list[index]);
                        }),
                    ),
                    );
                }
                }

                class ChannelItem extends StatelessWidget {
                final Map<String, dynamic>? item;
                const ChannelItem({super.key,required this.item});

                @override
                Widget build(BuildContext context) {
                    return Container(
                    // ignore: deprecated_member_use
                    color:Colors.blue,
                    alignment: Alignment.center,
                    child:Text(item?['name'] ?? "",style:TextStyle(color:Colors.white) ),
                    );
                }
                }

                // 优化后的 Dio 工具类
                class DioUtils {
                // 使用静态变量实现简单单例
                static final Dio _dio = Dio(BaseOptions(
                    baseUrl: 'https://geek.itheima.net/v1_0/',
                    connectTimeout: Duration(seconds: 100),
                    receiveTimeout: Duration(seconds: 100),
                ));

                DioUtils() {
                    // 避免重复添加拦截器
                    if (_dio.interceptors.isEmpty) {
                    _addInterceptors();
                    }
                }

                void _addInterceptors() {
                    _dio.interceptors.add(InterceptorsWrapper(
                    onRequest: (options, handler) => handler.next(options),
                    onResponse: (response, handler) {
                        // 这里的逻辑可以根据业务需求简化
                        handler.next(response);
                    },
                    onError: (e, handler) => handler.next(e),
                    ));
                }

                Future<Response> get(String url, {Map<String, dynamic>? params}) {
                    return _dio.get(url, queryParameters: params);
                }
                }
- 路由管理
    - 概述
        - 通过Navigator和Router来管理页面栈，实现页面跳转和返回
        - 步骤
            - 用户操作/代码调用
            - Navigator操作
                - push
                    - 新Router入栈
                    - 新页面显示维栈顶
                - pop
                    - 当前Router出栈
                    - 上一页面显示成为新栈顶
            - 页面状态更新
    - 基本路由
        - 场景：页面不多，跳转逻辑简单
        - 用法：跳转时创建MaterialPageRoute实例
        - ```
            import 'package:flutter/material.dart';

            void main() {
            runApp(MainPage());
            }

            class MainPage extends StatelessWidget {
            const MainPage({super.key});

            @override
            Widget build(BuildContext context) {
                return MaterialApp(
                home: ListPage(),
                );
            }
            }

            //列表页
            class ListPage extends StatefulWidget {
            const ListPage({super.key});

            @override
            State<ListPage> createState() => _ListPageState();
            }

            class _ListPageState extends State<ListPage> {
            @override
            Widget build(BuildContext context) {
                return Scaffold(
                appBar: AppBar(
                    title: const Text("列表页"),
                ),
                body: ListView.builder(
                    padding: EdgeInsets.all(10),
                    itemCount: 20,
                    itemBuilder: (BuildContext context, int index) {
                    return GestureDetector(
                        onTap:(){
                        print("点击了列表项${index+1}");
                        Navigator.push(context, MaterialPageRoute(builder: (context)=>DetailPage()));
                        },
                        child:Container(
                        color: Colors.blue,
                        margin: EdgeInsets.only(top: 10),
                        height: 100,
                        alignment: Alignment.center,
                        child: Text("列表项${index+1}",style: TextStyle(color: Colors.white,fontSize: 20,)),
                    )
                    );
                    },
                ),
                );
            }
            }

            class DetailPage extends StatefulWidget {
            const DetailPage({super.key});

            @override
            State<DetailPage> createState() => _DetailPageState();
            }

            class _DetailPageState extends State<DetailPage> {
            @override
            Widget build(BuildContext context) {
                return Scaffold(
                appBar: AppBar(
                    title: Text("详情页"),
                ),
                body: Center(
                    child:TextButton(onPressed: () {
                    print("返回列表项");
                    Navigator.pop(context);
                    }, child: Text("返回列表页")
                    )
                ),
                );
            }
            }
- Flutter项目
    - 创建web项目和git管理
    - 