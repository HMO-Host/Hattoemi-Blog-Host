---
title: Flutter学习笔记
date: 2021-03-7T11:59:30.000+08:00
tags: 
- Flutter
---

## 环境配置

> 由于我个人只有`Ubuntu 20.10`的环境(`OS X`的环境不可用),所以这里只进行`Linux`环境下的`Flutter`安装与环境配置

### SDK

> 我使用的是`VSCode`,而不是已经在我电脑里面的`Android Studio`或`IDEA`

__[中文官网](https://flutter.cn/docs/get-started/install/linux)有安装教程__

推荐使用`Snap`安装`Flutter`

```sh
sudo snap install flutter --classic
```

> 当`IDE`需要`Flutter SDK`路径时,可以使用以下命令
>
> ```sh
> flutter sdk-path
> ```

### IDE

__`VSCode`需要安装三个插件,其中`Flutter`插件安装时会自动安装`Dart`插件,后两个可选__

[![6KEZxH.png](https://s3.ax1x.com/2021/03/07/6KEZxH.png)](https://imgtu.com/i/6KEZxH)

[![6KAR58.png](https://s3.ax1x.com/2021/03/07/6KAR58.png)](https://imgtu.com/i/6KAR58)

[![6KGlG9.png](https://s3.ax1x.com/2021/03/07/6KGlG9.png)](https://imgtu.com/i/6KGlG9)

## 创建项目

__[中文官网]([中文官网](https://flutter.cn/docs/get-started/install/linux)有安装教程)有教程__

> __注：我安装了`IDEA`快捷键映射,可能会与你们``VSCode`的实际情况有差别__

按下`Alt`键，或通过`Ctrl + Shift + A`直接打开`命令面板`

在`查看(view) -> 命令面板(Command Palette)`输入`Flutter`

[![6KmiOH.png](https://s3.ax1x.com/2021/03/07/6KmiOH.png)](https://imgtu.com/i/6KmiOH)

选择第一个`New Application Project`

第一次会对`Flutter`进行初始化,运气不好就只能重装`Flutter SDK`了

__弹出这个窗口时就可以选择项目的主目录了__

[![6KnB28.png](https://s3.ax1x.com/2021/03/07/6KnB28.png)](https://imgtu.com/i/6KnB28)

> `Umbrella`是我个人的一个学习项目,里面是对于语言或框架的主流路线的学习代码

创建完成后,会有弹窗提示你是否要参与谷歌的调查问卷,这里不强制要求

> __注：当你在 `VSCode`中点击`No Devices`的时候，你也许看不到`Start iOS Simulator`选项,如果你使用`OS X`你可能得运行以下命令才能启动模拟器__
>
> ```sh
> open -a simulator
> ```

__[使用`Flutter`创建`Ubuntu`桌面应用程序](https://cn.ubuntu.com/blog/canonical-enables-linux-desktop-app-support-with-flutter-2)__

```bash
flutter config --enable-linux-desktop
```

通过同样方式创建`Flutter`项目或在已有项目下

```bash
flutter create .
```

## 文件目录

>  像`android`和`ios`之类的目录应该不用我说了

### lib

> 这个文件夹是用来存放`Flutter`的工程文件的，其中`main.dart`是项目的入口(最初且必须的)文件

[![6dle5d.png](https://s3.ax1x.com/2021/03/13/6dle5d.png)](https://imgtu.com/i/6dle5d)

### test

> 测试文件夹，用于存放测试文件，很重要的

[![6d1MFJ.png](https://s3.ax1x.com/2021/03/13/6d1MFJ.png)](https://imgtu.com/i/6d1MFJ)

### 配置文件(pubspec.yaml)

> 声明第三方库依赖

[![6d18Qx.png](https://s3.ax1x.com/2021/03/13/6d18Qx.png)](https://imgtu.com/i/6d18Qx)

## 第一次运行

> 我使用了真机来运行项目，你们可以看到`CAM AL00`的选项(Android Studio)

在`main.dart`的编辑窗口下按下`F5`进行`debug`

[![6d1wYd.png](https://s3.ax1x.com/2021/03/13/6d1wYd.png)](https://imgtu.com/i/6d1wYd)

事 后

[![6d8VVU.png](https://s3.ax1x.com/2021/03/13/6d8VVU.png)](https://imgtu.com/i/6d8VVU)

亦或是在`Android Studio`下选择使用`web`/`Pixle 3a`并按下`Shift + F10`启动

[![6d8JaD.png](https://s3.ax1x.com/2021/03/13/6d8JaD.png)](https://imgtu.com/i/6d8JaD)

[![6d8Mx1.png](https://s3.ax1x.com/2021/03/13/6d8Mx1.png)](https://imgtu.com/i/6d8Mx1)

`Google`真香

## Coding from scratch

### 先从理解示例开始

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        // This is the theme of your application.
        //
        // Try running your application with "flutter run". You'll see the
        // application has a blue toolbar. Then, without quitting the app, try
        // changing the primarySwatch below to Colors.green and then invoke
        // "hot reload" (press "r" in the console where you ran "flutter run",
        // or simply save your changes to "hot reload" in a Flutter IDE).
        // Notice that the counter didn't reset back to zero; the application
        // is not restarted.
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".

  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      // This call to setState tells the Flutter framework that something has
      // changed in this State, which causes it to rerun the build method below
      // so that the display can reflect the updated values. If we changed
      // _counter without calling setState(), then the build method would not be
      // called again, and so nothing would appear to happen.
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called, for instance as done
    // by the _incrementCounter method above.
    //
    // The Flutter framework has been optimized to make rerunning build methods
    // fast, so that you can just rebuild anything that needs updating rather
    // than having to individually change instances of widgets.
    return Scaffold(
      appBar: AppBar(
        // Here we take the value from the MyHomePage object that was created by
        // the App.build method, and use it to set our appbar title.
        title: Text(widget.title),
      ),
      body: Center(
        // Center is a layout widget. It takes a single child and positions it
        // in the middle of the parent.
        child: Column(
          // Column is also a layout widget. It takes a list of children and
          // arranges them vertically. By default, it sizes itself to fit its
          // children horizontally, and tries to be as tall as its parent.
          //
          // Invoke "debug painting" (press "p" in the console, choose the
          // "Toggle Debug Paint" action from the Flutter Inspector in Android
          // Studio, or the "Toggle Debug Paint" command in Visual Studio Code)
          // to see the wireframe for each widget.
          //
          // Column has various properties to control how it sizes itself and
          // how it positions its children. Here we use mainAxisAlignment to
          // center the children vertically; the main axis here is the vertical
          // axis because Columns are vertical (the cross axis would be
          // horizontal).
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ), // This trailing comma makes auto-formatting nicer for build methods.
    );
  }
}

```

首先看到第一行

```dart
import 'package:flutter/material.dart';
```

这是使用`Flutter`进行开发的必要语句，它的意思是"导入`Flutter`包"

因为`dart`本质是一个语言，而`Flutter`是使用`dart`语言的UI工具包

接下来是这个方法

```dart
void main() {
  runApp(MyApp());
}
```

`void`是指不返回值

这是个`main`(入口)方法

就像要打开神奇的洞穴要大喊"芝麻开门"一样，要使用`Flutter`这是必须的

同时它可以写成

```dart
void main()=>runApp(MyApp());
```

而其中的`MyApp`，也就是下面的

```dart
class MyApp extends StatelessWidget {
// 此处省略
}
```

这是创建了一个`类(class)`叫做`MyApp`，它通过`extends`关键字`继承`了`StatelessWidget`这个类

让我们回到这句话

```dart
runApp(MyApp());
```

其中`runApp`是一个`方法`，它`实例化`了`MyApp`这个`类`，实例化可以写上`new`关键字，但也可以省略

```dart
runApp(new MyApp());
```

__那么为什么不直接写成`void main()=>runApp(StatelessWidget());`呢？__

首先，为了未来维护代码，你不应该把它写成一行，而且写成一行并不会带来可见的性能提升

其次，你通常会写很多元素，这会导致它非常大，为了易读性(代码是给人看的)，你应该创建一个类(自定义组件)，并在里面按照编码规范进行开发

__需要注意的是__

方法首字母小写，下一个单词首字母大写，也就是[驼峰命名法](https://baike.baidu.com/item/%E9%AA%86%E9%A9%BC%E5%91%BD%E5%90%8D%E6%B3%95)，而类则全部单词的首字母大写

__那么`StatelessWidget`是什么呢？__

它`Flutter`提供的一个组件(类)，是`无状态组件`，它的状态不可变，而且它是一个`抽象类`，它有一个`抽象方法`叫`build`

而`StatefulWidget`是之后会提到的`有状态组件`，它的状态可能在`widget生命周期`改变

__那么这个叫做"build"的抽象方法是干嘛用的？__

首先，抽象方法是“只有名字没有具体功能”的方法

它要求每个继承它的类都要强制实现这个方法

__那么让我们回到示例中的代码__

```dart
@override
Widget build(BuildContext context) {
  return MaterialApp(
    title: 'Flutter Demo',
    theme: ThemeData(
      // This is the theme of your application.
      //
      // Try running your application with "flutter run". You'll see the
      // application has a blue toolbar. Then, without quitting the app, try
      // changing the primarySwatch below to Colors.green and then invoke
      // "hot reload" (press "r" in the console where you ran "flutter run",
      // or simply save your changes to "hot reload" in a Flutter IDE).
      // Notice that the counter didn't reset back to zero; the application
      // is not restarted.
      primarySwatch: Colors.blue,
    ),
    home: MyHomePage(title: 'Flutter Demo Home Page'),
  );
}
```

`Widget`是一个组件(类)

而这个`bulid`方法就是返回`Widget`这个组件的(子类)方法，所以要在关键字`return`后面返回一个组件

而示例中的组件就是`MaterialApp`，有一定`Android`开发经验(没有经验的同学也看过来)的同学一定联想到了`material design`↖(^ω^)↗

没错，这就是基于`material design`的`Flutter`组件

---

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议</a>进行许可。