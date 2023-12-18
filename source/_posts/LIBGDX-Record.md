---
title: LIBGDX 学习记录（1）
---

# LIBGDX 学习记录（1）
> 认识libgdx

### 介绍
><b>libGDX</b> is a cross-platform Java game development framework based on OpenGL (ES), designed for Windows, Linux, macOS, Android, web browsers, and iOS. It provides a robust and well-established environment for rapid prototyping and iterative development. Unlike other frameworks, libGDX does not impose a specific design or coding style, allowing you the freedom to create games according to your preferences.<br><br>
github： https://github.com/libgdx/libgdx
<br>
---
### 准备工作
1. JDK： 建议 11-18. 我个人使用JDK11，感觉非常良好
2. 开发工具，正常的java开发集成工具都可以，我个人使用JetBrain的Idea
3. 依赖管理工具，libgdx使用的是gradle进行包管理，所以最好提前安装gradle。我本地安装的是7.4.2. 如果不提前手动下载，后面导入可能会麻烦一些。
4. 初始化项目：
    * 下载官方的初始化工具，目前地址： https://libgdx.com/wiki/start/project-generation （最新版）
    * 或者可以下载 1.10 版，因为我就是用这个版本开发的。https://github.com/libgdx/libgdx/releases 可以在这里找到历史版本，选择1.10.0即可。

### Init!
好了，现在我们可以尝试开始我们的第一个项目了。<br> 
<br>
首先，打开我们刚刚下载好的初始化工具： <br>
![init01](Libgdx_Init01.png)
<br>
关于第6点打包模式，个人建议勾选desktop，方便桌面调试，或者直接开发桌面应用。andriod也推荐勾选，因为这个引擎起始主要是为了andriod游戏而做的，大部分资源文件都会放在andriod项目下。不管你开发的是什么应用。<br>
至于更多的第三方依赖，暂时用不到，可以不需要管。然后，我们直接点击generate生成即可.<br>
点击生成后，会自动在目标文件夹下生成初始化的代码，并且会尝试使用gradle导入依赖，但是此时极有可能因为本地JAVA_HOME等原因导入失败，这个失败我们可以先不去管，忽略它，直接使用我们的开发工具（我使用的IDEA）打开该项目即可。<br>
在使用我们的开发工具打开项目后，首先建议修改默认的gradle配置，更改为自己下载好的版本。
![init02](Libgdx_Init02.png)<br>
这样，导入依赖会更快更方便，不然的话，我本地实测会比较慢。<br>
然后接下来就让gradle自动构建就可以了。

### Start!
构建好之后，项目看起来应该是这个样子的:
![init03](Libgdx_Init03.png)<br>
其中，desktop目录中，存在一个名为DesktopLauncher的启动类，我们可以直接运行这个启动类。应该会看到一个应用程序启动，如下图：<br>
![init04](Libgdx_Init04.png)<br>
如果看到这个画面，恭喜你，我们已经成功的初始化了一个游戏！

---
### Hello World
现在我们看到的仅仅是一个libgdx logo的图片以及红色背景。这显然不是我们最终想要的，我们至少想要一个自己的**hello world**<br>
我们就需要认识一下core文件夹，下面有一个初始化自带的一个Class，MyGdxGame，它长这个样子：
```java
package com.mygdx.game;

import com.badlogic.gdx.ApplicationAdapter;
import com.badlogic.gdx.graphics.Texture;
import com.badlogic.gdx.graphics.g2d.SpriteBatch;
import com.badlogic.gdx.utils.ScreenUtils;

public class MyGdxGame extends ApplicationAdapter {
	SpriteBatch batch; // 画笔，或者说专门画图片(Sprite)的画笔
	Texture img; // 图片，我们看到的libgdx logo 就是它
	
	@Override
	public void create () { // 当前类初始化的方法
		batch = new SpriteBatch(); // 初始化画笔
		img = new Texture("badlogic.jpg"); // 初始化 加载 图片
	}

	@Override
	public void render () { // 渲染函数，可以理解为程序的每一帧需要做什么，这里也是程序的主逻辑
		ScreenUtils.clear(1, 0, 0, 1); // 设置屏幕背景色
		batch.begin();
		batch.draw(img, 0, 0); //  使用画笔绘制图片，图片的位置指定在 （0，0） 处
		batch.end();
	}
	
	@Override
	public void dispose () { // 销毁方法，程序运行中的许多资源（Disposable）都需要释放
		batch.dispose();
		img.dispose();
	}
}
```
当前程序本质就是每一帧都会循环调用render函数，我们要做的，也就是在render函数中编写我们自己的逻辑即可。

### 参考
[官方文档](https://libgdx.com/wiki/start/project-generation)<br>
[官方simple教程](https://libgdx.com/wiki/start/a-simple-game)