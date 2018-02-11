 ## Kotlin新的征程（一）

![](https://upload-images.jianshu.io/upload_images/9352581-95332e208344727a.png)    

自今年**Google**宣布将Kotlin作为Android首选开发语言（官方语言），我就知道Kotlin即将要崛起，为什么会崛起？因为Kotlin这门语言不仅可以针对Android移动开发，它还可以：
 * Web前端开发
 * Web后端开发
 * Server脚本
 * 桌面游戏  
   
为什么选择Kotlin？
 * 简洁： 大大减少样板代码数量
 * 安全：避免空指针异常等整个类的错误
 * 互操作性：充分利用JVM，Android和浏览器的现有库
 * 工具友好：可以用任何Java IDE或者使用命令行构建
 
而且Kotlin还有着强大的Spring 框架，Gradle 构建脚本，等的支持 
是不是很强大？你害不害怕？     
没关系下面我们一起来认识它吧！

### Kotlin 是什么鬼？

Kotlin是一种在Java虚拟机上运行的静态类型编程语言，它也可以被编译成为JavaScript源代码。它主要是由俄罗斯圣彼得堡的JetBrains开发团队所发展出来的编程语言，其名称来自于圣彼得堡附近的科特林岛。2012年1月，著名期刊《Dr. Dobb's Journal》中Kotlin被认定为该月的最佳语言。虽然与Java语法并不兼容，但Kotlin被设计成可以和Java代码相互运作，并可以重复使用如Java集合框架等的现有Java类库。


### Kotlin 的历史

2011年7月，JetBrains推出Kotlin项目，这是一个面向JVM的新语言，它已被开发一年之久。JetBrains负责人Dmitry Jemerov说，大多数语言没有他们正在寻找的特性，Scala除外。但是，他指出了Scala的编译时间慢这一明显缺陷。Kotlin的既定目标之一是像Java一样快速编译。2012年2月，JetBrains以Apache 2许可证开源此项目。

Jetbrains希望这个新语言能够推动IntelliJ IDEA的销售。

Kotlin v1.0于2016年2月15日发布。这被认为是第一个官方稳定版本，并且JetBrains已准备从该版本开始的长期向后兼容性。

在Google I/O 2017中，Google宣布在Android上为Kotlin提供最佳支持。


还记得刚开始接触Java这门语言的时候，我认识了Java之父——詹姆斯·高斯林（James Gosling） ，看到过一个很有意思的问题，在Java里面的对象传递的到底是传址还是传值？（这是个有争论的问题），普通人可能会很平常的说，是传值！但是我会说：“是传值，詹姆斯——高斯林的想法也是和我一样的。” 的确java之父也是这样以为的,因为地址也是值! 我觉得有水平一点的人对一门语言的历史，创始人，这些都是有一些研究的。我想这两种答案给别人留下的影响映像是有一定差距的，大家应该也能感受得到！

最后普及一个Android 之父——安迪·鲁宾（Andy Rubin），现在好像也去做手机了，但愿他能成为下一位雷军，毕竟笔者现在是一位Android Developer 在这里稍微点一嘴！


### Kotlin的优势

* 函数式编程范式 
* 高阶函数
* Streams API
* 全面支持Lambda表达式
* 数据类 (Data classes) 
* 函数字面量和内联函数（Function literals & inline functions）
* 函数扩展 (Extension functions)
* 空安全（Null safety）
* 智能转换（Smart casts）
* 字符串模板（String templates）
* 主构造函数（Primary constructors）
* 类委托（Class delegation）
* 类型推断（Type inference）
* 单例（Singletons）
* 声明点变量（Declaration-site variance）
* 区间表达式（Range expressions）

在这里不详细说明了，在以后会慢慢的讲解，毕竟心急吃不了热豆腐，人一生下来不可能学几天就会说话了，这都是一个过程，有的人可能悟性高看一遍两遍就学会了，悟性低一点的小伙伴也要加油，龟兔赛跑的游戏在这里轻轻点激你们一下，加油！

![Kotlin是世界上最好的语言](https://upload-images.jianshu.io/upload_images/9352581-d0b361966de35d16.jpg)

### 总结：

总而言之Kotlin就是一门即将走向未来的语言，在这里我会说Kotlin是世界上最好的语言！不服的可以点个喜欢，谢谢！