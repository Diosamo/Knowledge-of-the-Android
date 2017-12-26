# AndroidStudio3.0快速环境安装使用
![](http://upload-images.jianshu.io/upload_images/9352581-55c98003e900ddd7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Android Studio 也称 AS  是一个Android集成开发工具，是我们现在Android开发者必须学会使用的开发工具,当然也有其他的一些开发工具可以开发Android应用,但是原生的开发,AS就是武林萌主!  

大家可以先通过下面链接,开始下载,一边下,一边继续向下看!   

[Android Studio中文社区(官网)](http://www.android-studio.org/)   
[JavaJDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk9-downloads-3848520.html)  

记得下载Studio和JDk的时候 根据自己使用的系统下载对应的版本!  

### 简介:  

AndroidStudio 是JetBrains这一家很牛逼的公司开发的,为什么说这家公司牛逼呢?因为现在很多主流的开发工具都是这家公司做的,最为人熟知的是Intellij IDEA,并且AS 3.0的官方推荐语言Kotlin 也是这家公司的,语言和工具都出处一处,他们之间的默契在这里可想而知! 


### 环境配置   

大家要一步一步来,不要忽略每一步,有可能就让你的使用产生错误!  

1.将下载好的JDK安装(记得安装的目录)  

[图片上传失败...(image-5f10d1-1514257015798)]  

2.安装完成以后配置环境变量   

鼠标右键点击计算机会出现这样一个界面   
![](http://upload-images.jianshu.io/upload_images/9352581-5e8249c1c02018b1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

点击高级系统设置       

![](http://upload-images.jianshu.io/upload_images/9352581-15ee7a346f45f95a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)    

点击环境变量  
![](http://upload-images.jianshu.io/upload_images/9352581-cdb9c61da23bedd7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

然后找到path,这个路径也就是刚刚安装的Jdk下面的bin目录(记住是JDK不是JRE),将路径放入变量值中,注意不要把以前的变量值直接换成了你现在copy的路径,应该在以前的变量值前面加上  
![](http://upload-images.jianshu.io/upload_images/9352581-7cec953f7bcc0832.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

最后以分号结束;   然后确定确定.  
![](http://upload-images.jianshu.io/upload_images/9352581-619323b14a7e0b8b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

好了环境装好了,接下来就安装AS了.   


### AndroidStudio 安装

1.打开下载好的AndroidStudio 安装文件.  

![](http://upload-images.jianshu.io/upload_images/9352581-20c9f1ae37b05833.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

2.然后next直到这里,选择安装的路径  

![](http://upload-images.jianshu.io/upload_images/9352581-40503758f3c464bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.选择好后一路next,然后install.完成打开AS  

![](http://upload-images.jianshu.io/upload_images/9352581-2d7c38a53f385422.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.启动AS后会出现下图,如果以前没有用过AS的直接勾选下面,有的可以自己导入自己的配置.最后点击Ok.

![](http://upload-images.jianshu.io/upload_images/9352581-becb0b041bbccd15.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. 启动的时候可能会出现下图,直接点击cancel,然后进入到了AS安装向导界面   

![](http://upload-images.jianshu.io/upload_images/9352581-2b15ac85639476db.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6.点击next进入UI界面主题选择界面，可以选择自己喜欢的风格，这里选择Darcula风格   

![](http://upload-images.jianshu.io/upload_images/9352581-a7b08e53c3311f3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



7.这里需要指定SDK的本地路径，如果之前电脑中已经存在SDK，可以指定该路径，后续就可以不用下载SDK；我这里演示本地没有安装过SDK的场景，这里暂时可以指定一个后续将保存SDK的路径；  


![](http://upload-images.jianshu.io/upload_images/9352581-7932d7997a101835.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

8.如果提示No Android SDK found ,点击next,然后点击finish ,AS会自动开始下载,下载完成后点击会出现如下界面,点击finish    

![](http://upload-images.jianshu.io/upload_images/9352581-a1d8907121cc3ccd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

9.下载完成SDK后，点击Finish进入AS的欢迎界面

![](http://upload-images.jianshu.io/upload_images/9352581-ad6e0ec81acd7dc9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

10.配置AS第一次运行环境，并且能成功编译运行一个APP，以helloworld为例。  
点击上图中的Start a new Android Studio project新建一个工程，进入下面的界面   

![](http://upload-images.jianshu.io/upload_images/9352581-180375b741356117.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后一路next就成功创建了一个最简单的项目了! 恭喜你成功学会构建AndroidStudio3.0的使用环境,以后会对AS进行详细的说明!





