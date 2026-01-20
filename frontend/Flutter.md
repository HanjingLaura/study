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