# SizeClassesDemo
### 一、什么是SizeClasses

SizeClasses 是从iOS 8开始，Apple在应用界面的可视化设计上添加的一个新的特性。

SizeClasses认为：对于任何设备来说，界面的宽度和高度都只分为三种描述：紧凑，任意和宽松。这样开发者便可以无视设备具体的尺寸，而是对这两类和它们的组合进行适配。

Apple共推出了frame 、autoresizing、autolayout、SizeClasses等布局方式。
*  frame：直接写坐标。
* autoresizing： 根据父控件frame发生改变,子控件跟着一起改变。
* autolayout：自动布局。
* size Classes：发现屏幕变的太多样化,界面不得不统一。

```SizeClasses仅仅是对屏幕进行了分类, 真正排布UI元素还得使用autolayout。```

使用了SizeClasses不再有横竖屏的概念, 只有屏幕尺寸的概念；不再有具体尺寸的概念, 只有抽象尺寸的概念。

### 二、SizeClasses的表示方法

**SizeClasses把宽度和高度各分为3种情况**
1. Compact : 紧凑(小)
2. Any : 任意
3. Regular : 宽松(大)

**SizeClasses表示与设备屏幕对应关系**

1. iPhone4S,iPhone5/5s,iPhone6
* 竖屏：(w:Compact h:Regular)
* 横屏：(w:Compact h:Compact)

2. iPhone6 Plus
* 竖屏：(w:Compact h:Regular)
* 横屏：(w:Regular h:Compact)

3. iPad
* 竖屏：(w:Regular h:Regular)
* 横屏：(w:Regular h:Regular)

4. Apple Watch(猜测)
* 竖屏：(w:Compact h:Compact)
* 横屏：(w:Compact h:Compact)

以上关系不必记住，打开底部的编辑器通，过点击各手机、屏幕方向，就能查看横竖屏情况下w和h的表示方法。
比如在iPhone8 plus的横屏下是w:R h:C。
![w:R h:C](https://upload-images.jianshu.io/upload_images/1966717-ae8ae86f5e264785.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 三、SizeClasses的使用方法
一般情况下，一个IB(xib/storyboard)文件会是一个竖屏显示的某机型显示效果，你所添加的约束，会是所有机型所有屏幕方向上的约束。你可以通过底部的view as进行切换机型和屏幕方向进行效果预览。

想要添加其他机型或者屏幕方向上的约束，需要先进去编辑模式，点击view as后，出现如下图的面板
![编辑面板](https://upload-images.jianshu.io/upload_images/1966717-5072d619463a1039.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

通过点击“❓”可以查看Apple的文档，用白话来讲，步骤就是
1. 在view as选择当前的模式
2. 点击Vary  for  Traits选择编辑模式
3. 查看受影响的模式
4. 进入编辑模式进行编辑，然后结束编辑
这个时候就可以对约束进行编辑了。

点击Vary for Traits进入编辑模式，弹出了Width和Height选项，前面打对号就锁定当前的这个属性。

![Vary for Traits](https://upload-images.jianshu.io/upload_images/1966717-00433949f636111f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

选取确定之后整个SizeClasses选项框就变成蓝色的，也就是进入了编辑模式。点击任意位置能让弹窗消失。
![蓝色表示进入了编辑模式](https://upload-images.jianshu.io/upload_images/1966717-62a7aeeeb609aa78.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**注意：**
只有当您进入了编辑模式，才能对特殊模式下的约束进行增删改等操作，否则约束将添加到所有的模式下。

在view as里切换效果后，可在约束里通过点选切换Constrats选项，看到当前模式或者所有模式的约束。
但是通过切换只是查看此模式的约束，而**不是进入当前模式的编辑状态**！
![约束](https://upload-images.jianshu.io/upload_images/1966717-05db2e62aaef7990.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 四、Vary  for  Traits 怎么选
通过点击Vary for Traits进入编辑模式，弹出了Width和Height选项，前面打对号就锁定当前的这个属性。
锁定模式后，就可以开始编辑约束，这些约束就会在当前受影响的显示模式下生效。

比如已经锁定了当前模式为w:Regular h:Compact：
根据本文```[二、SizeClasses的表示方法]```中```[SizeClasses表示与设备屏幕对应关系]```可知，
锁定了w:Regular h:Compact模式后编辑的约束，将会对iphone的Plus机型横屏模式生效。

举几个例子来说明Vary  for  Traits 该怎么选：

#### 1. 什么都不选
![默认](https://upload-images.jianshu.io/upload_images/1966717-807261e68a1f1770.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
什么都不选的时候，默认为（*，*），即通用界面，所有尺寸设备通用。我们通过Device和Orientation可以组合出所有尺寸设备的横竖屏情况。

#### 2. 在**view as**选择显示**wC**的时候选择Width
即竖屏模式下，选择Width，表示锁定当前Width的模式，即表示(C，*)。

![wC时锁定Width](https://upload-images.jianshu.io/upload_images/1966717-bd83f400bc3fce9d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

(C，*)的显示模式有（C，C）和（C，R），通过Size Class类型判断可以得到是20种:
1) iPhone竖屏 （C，R）5种
2) iPhone横屏 （C，C）4种
3) iPad splitView下，显示区域小于2/3的，（C，R）11种

当然，编辑面板中的显示，受影响的模式确实为20种，可以通过点击查看受影响的模式有哪些。

#### 3. 在**view as**上显示**hC**的时候选择Height
即横屏模式下，选择Height，表示锁定当前Height的模式，表示（*，C）。

![hC时锁定Height](https://upload-images.jianshu.io/upload_images/1966717-2705ecc46c3ac5cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

(*，C)的显示模式有（C，C）和（R，C），通过Size Class类型判断可以得到是26种:
原理一样，不再列举，自行动手查看结果。

**其他情况不再列举，自己动手，丰衣足食**

DEMO代码下载：[https://github.com/xueyongwei/SizeClassesDemo](https://github.com/xueyongwei/SizeClassesDemo)





