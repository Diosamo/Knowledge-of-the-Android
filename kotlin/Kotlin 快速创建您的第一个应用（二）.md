## Kotlin 快速创建您的第一个应用（二）

上一次对Kotlin进行的大致的介绍[kotlin 新的征程(一)](https://www.jianshu.com/p/c7a8cadcbd8b)   

那么今天呢,我们要干什么?
![](http://upload-images.jianshu.io/upload_images/9352581-b8c09487368a2ee1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

今天,我们就要开始学习Kotlin 的一些语法了,不管你是编程大神,还是刚入门的fish,不管你以前用的是Java,还是PHP.我相信你都可以很快学会这门简洁,精炼的语言. 当然如果你是小白,那么恭喜你,你学起这么语言将不会受到其他语言的思维限制,学习起来将会更加轻松. (只针对Android)  

**下面我将直接开门见山,各位速度上车**:

首先你需要配置好你的开发[AndroidStudio 3.0快速环境安装使用](https://github.com/Diosamo/Knowledge-of-the-Android/blob/master/AndroidStudio 3.0快速环境安装使用.md) 

当各位安装好了AS以后下面我会灰常详细的带你们进行Android开发的道路,我相信你敲一遍不行?那么敲一百遍,奇异自现(开个玩笑) 小伙伴们只要努力就可以了!

### 开始实战:
 
![](http://upload-images.jianshu.io/upload_images/9352581-6429b351a43f6bd7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)   

首先开始一个新的项目   

![](http://upload-images.jianshu.io/upload_images/9352581-2b8450871a7e5854.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

填写好自己的配置,然后next 

![](http://upload-images.jianshu.io/upload_images/9352581-35db5e5431527d58.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)   

这里红色的标记是最低支持的版本Api19,也就是Android版本4.4其他的就是一些开发Android眼镜,手表,电视等一些设备选择的(Android不止是手机的系统,在很多智能设备上都有Android的身影),这里不做讲解了,继续next   

![](http://upload-images.jianshu.io/upload_images/9352581-2b2255ddb2076549.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](http://upload-images.jianshu.io/upload_images/9352581-6df044cf986b844d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上面两个界面直接点击next,finish,恭喜你项目已经创建好了

![](http://upload-images.jianshu.io/upload_images/9352581-b397525a6423a7fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

 然后可能你会出现和我一样的这个界面,但是这个界面的代码并不是Kotlin的代码,它是Java代码!  

什么鬼?我们不是要学Kotlin吗?  

不要慌同学们,3.0 的AS可以一键转换为Kotlin的代码,很简单你只需要按住Ctrl+Shift+Alt +K ! 是不是很神奇,秒转对吗!想要变回去吗,对不起,变不回去了,Java代码是可以转Kotlin的但是Kotlin没有办法转换成Java.在这里给大家点一嘴,Java是一门面向对象语言,而Kotlin是既有面向对象又具有函数式结构,并且可以多种风格使用.

![](http://upload-images.jianshu.io/upload_images/9352581-d181c14a7bb81a3a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果是和我上面图片一样的同学你可以点击按钮运行了!

![](http://upload-images.jianshu.io/upload_images/9352581-b33dce2a344f5a54.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  


运行的时候可以点击你对应的版本的模拟器,这里我建好了很多,当然也可以使用你自己的Android真机连接USB,然后打开手机的开发者模式中的USB调试(有的时候可能看不见,可能被电脑上面的一些其他软件抢走了adb 调试桥,这里需要把一些什么豌豆荚,手机助手之类的多余的软件关闭掉,然后重新插拔手机,或者用Adb 命令,需要将你的path配置好,这里就不多说了,不会的百度,Google 一下都是可以的.)   

![](http://upload-images.jianshu.io/upload_images/9352581-6a85ecfcc6b7d341.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

恭喜你成功的做好了你的第一个Kotlin应用!下一章我们就要真正的开始学习Kotlin的语法,基于项目去做一些讲解了哦!


