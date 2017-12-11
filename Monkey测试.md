## Andorid自动化测试Monkey

### Mokey环境:
首先配置好ADB环境,ADB是什么?  
[ADB简介](https://jingyan.baidu.com/article/0320e2c1cc7a031b87507b91.html)  
[ADB环境配置](https://jingyan.baidu.com/article/17bd8e52f514d985ab2bb800.html)  
通过上面将最基本的Mokey使用环境搭建好以后在进行学习和测试.


### Monkey是什么?

Monkey 其实是AndroidSDk中附带的一个工具,它的意思是猴子,也就是猴子派来的逗比,玩起手机来不按套路出牌,对着手机屏幕疯狂输出.好了搞搞前面的是几句大白话.言归正传, Monkey测试是Android自动化测试的一种手段，Monkey测试本身非常简单，就是模拟用户的按键输入，触摸屏输入，手势输入等，看设备多长时间会出异常。 

### Monkey程序介绍
（1） Monkey程序由Android系统自带，使用Java诧言写成，在Android文件系统中的存放路径是： /system/framework/monkey.jar；   
（2） Monkey.jar程序是由一个名为“monkey”的Shell脚本来启动执行，shell脚本在Android文件系统中 的存放路径是：/system/bin/monkey；  
（3）Monkey 命令启动方式：    
a）可以通过PC机CMD窗口中执行: adb shell monkey ｛+命令参数｝来进行Monkey测试          

b）在PC上adb shell 进入Android系统，通过执行 monkey {+命令参数} 来进行Monkey 测试          

c )  在Android机或者模拟器上直接执行monkey 命令，可以在Android机上安装Android终端模拟器  



### Mokey架构

![farmwork](http://images2015.cnblogs.com/blog/263119/201605/263119-20160505223944482-1516389266.png)



### Monkey 命令:

* 标准的monkey 命令 
最简单的方法就是用用下面的命令来使用Monkey，这个命令将会启动你的软件并且触发500个事件. 

	$ adb shell monkey -v -p your.package.name 500

[adb shell] monkey [options] , 例如：  
adb shell monkey -v 500 ——–产生500次随机事件，作用在系统中所有activity（其实也不是所有的activity，而是包含Intent.CATEGORY_LAUNCHER或Intent.CATEGORY_MONKEY 的activity）。
 
上面只是一个简单的例子，实际情况中通常会有很多的options 选项 
四大类—— 常用选项 、 事件选项 、 约束选项 、 调试选项 

1. ：常用选项  
–help：打印帮助信息 
-v：指定打印信息的详细级别，一个 -v增加一个级别 ， 默认级别为 0 。  
2. ：事件选项  
-s：指定产生随机事件种子值，相同的种子值产生相同的事件序列。如：

  -s 200 –throttle：每个事件结束后的间隔时间——降低系统的压力（如不指定，系统会尽快的发送事件序列）。如：–throttle 100     
–pct-touch：指定触摸事件的百分比，如：–pct-touch 5% ， 相关的还有以下option： 
–pct-motion （滑动事件）、    
–pct-trackball （轨迹球事件） 、   
–pct-nav （导航事件 up/down/left/right）、  
–pct-majornav (主要导航事件 back key 、 menu key)、  
–pct-syskeys (系统按键事件 Home 、Back 、startCall 、 endCall 、 volumeControl)、   
–pct-appswitch （activity之间的切换）、   
–pct-anyevent （任意事件）    
3. ：约束选项   
复制代码 代码如下:  

-p：指定有效的package（如不指定，则对系统中所有package有效），一个-p 对应一个有效package， 如：-p com.ckt -p com.ckt.asura；   
-c：activity必须至少包含一个指定的category，才能被启动，否则启动不了；   
4. ：调试选项   
复制代码 代码如下:

–dbg-no-events：初始化启动的activity，但是不产生任何事件。   
–hprof：指定该项后在事件序列发送前后会立即生成分析报告 —— 一般建议指定该项。   
–ignore-crashes：忽略崩溃   
–ignore-timeouts：忽略超时   
–ignore-security-exceptions：忽略安全异常   
–kill-process-after-error：发生错误后直接杀掉进程   
–monitor-native-crashes：跟踪本地方法的崩溃问题   
–wait-dbg：知道连接了调试器才执行monkey测试。  


### Demo monkey命令： 
复制代码 代码如下:   
adb shell monkey -p com.xy.android.junit -s 500 -v 10000   
但是，工作中为了保证测试数量的完整进行，我们一般不会在发生错误时立刻退出压力测试。monkey 测试命令如下   
复制代码 代码如下:   
adb shell monkey -p com.xy.android.junit -s 500 –ignore-crashes –ignore-timeouts –monitor-native-crashes -v -v 10000 > E:\monkey_log\java_monkey_log.txt


### Monkey结果输出
      1.保存在pc中 adb shell monkey [option] <count> >d:\monkey.txt
      2.保存在手机中 adb shell monkey [option] <count> >/mnt/sdcard/monkey.txt
      3.标准流与错误流分开保存  monkey [option] <count> 1>/mnt/sdcard/monkey.txt 2>/mnt/sdcard/error.txt


### 总结:

在Monkey测试完成以后，在应用上线前,必须把所有的Crash都修复掉,因为任何一个Crash都可能导致用户的体验变差.  
[如有更好的建议提议,可以发到我的邮箱diosamolee2014@gmail.com](#)