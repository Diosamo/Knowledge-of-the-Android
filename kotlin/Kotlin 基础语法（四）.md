## Kotlin Kotlin 实战语法（四）  

上一次大家学会了Kotlin的基本数据类型 [Kotlin 基本数据类型（三）](https://www.jianshu.com/p/62aaa097f09a)  

今天呢我们正式开始Kotlin的语法学习！注意了语法是一本编程语言的重中之重哦！所以集中注意力，我们开始吧！

![](http://upload-images.jianshu.io/upload_images/9352581-8e24994743c0bd62.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### Kotlin基础语法：

Kotlin 文件都是以 .kt 为后缀。
![](http://upload-images.jianshu.io/upload_images/9352581-ee0b23872f00786d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

怎么在AS里面创建Kotlin文件呢？很简单只需要点击你所要指定的包下，然后右键选择New，然后选择Kotlin File/Class 
![](http://upload-images.jianshu.io/upload_images/9352581-42e6bb14acd9d0c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#### 包声明：  
![](http://upload-images.jianshu.io/upload_images/9352581-ecef8247de4140d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

kotlin源文件不需要相匹配的目录和包，源文件可以放在任何文件目录。  

以上例中 test() 的全名是 com.kotlin.test 是这个目录下面的一个函数。  
MyOne 的全名是 com.kotlin.MyOne 是这个目录下的一个类。  
import是导包的意思，就是导入包以后可以使用包下面的共有资源。  
如果没有指定包，默认为 default 包。  

### 默认导入：
有多个包会默认导入到每个 Kotlin 文件中：

kotlin.*
kotlin.annotation.*
kotlin.collections.*
kotlin.comparisons.*
kotlin.io.*
kotlin.ranges.*
kotlin.sequences.*
kotlin.text.*

### 函数定义：

1.Kotlin中函数使用关键字fun，函数中的参数需要指定类型，使用参数：类型的格式去制定。

![](http://upload-images.jianshu.io/upload_images/9352581-be05d016cab9e76b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

2.表达式作为函数体，返回类型自动推断：  

![](http://upload-images.jianshu.io/upload_images/9352581-2d65b54215d1e000.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

3.无返回值的函数(类似Java中的void)：  

![](http://upload-images.jianshu.io/upload_images/9352581-3b807f43bd00cc69.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 可变参数函数：  
可变参数是什么呢？其实很简单就是可以无限传入指定类型的参数，不管多少个！   

函数的可变参数可以用 vararg 关键字进行标识：   

下列代码是将传入的参数打印，可以看见不管是传入多少个都是可以的！
![](http://upload-images.jianshu.io/upload_images/9352581-40ef8619d729dd66.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/9352581-f07ccc12bc851d3b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### lambda(匿名函数)： 

![](http://upload-images.jianshu.io/upload_images/9352581-38b189c003869ecd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

lambda表达式会让代码大大减少，不过可读性自然也就下降，初学者不建议多使用！

### 定义常量与变量

可变变量定义：var 关键字   

    var <标识符> : <类型> = <初始化值>

不可变变量定义：val 关键字，只能赋值一次的变量(类似Java中final修饰的变量)  

    val <标识符> : <类型> = <初始化值>

常量与变量都可以没有初始化值,但是在引用前必须初始化

编译器支持自动类型判断,即声明时可以不指定类型,由编译器判断。

![](http://upload-images.jianshu.io/upload_images/9352581-b85420c4c709110b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 注释: 
Kotlin 支持单行和多行注释，实例如下：  

    // 这是一个单行注释
    
    /* 这是一个多行的
     块注释。 */

### 字符串模板:

$ 表示一个变量名或者变量值

$varName 表示变量值

${varName.fun()} 表示变量的方法返回值:

![](http://upload-images.jianshu.io/upload_images/9352581-5b71be90329bd311.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这是最后的值 ： S2="a was 1, but now is 2"

### NULL检查机制  

Kotlin的空安全设计对于声明可为空的参数，在使用时要进行空判断处理，有两种处理方式，字段后加!!像Java一样抛出空异常，另一种字段后加?可不做处理返回值为 null或配合?:做空判断处理

![](http://upload-images.jianshu.io/upload_images/9352581-4bddf0d72b06fc8b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

当一个引用可能为 null 值时, 对应的类型声明必须明确地标记为可为 null。

当 str 中的字符串内容不是一个整数时, 返回 null:
![](http://upload-images.jianshu.io/upload_images/9352581-a364ced9c0c09300.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 类型检测及自动类型转换：  

我们可以使用 is 运算符检测一个表达式是否某类型的一个实例(类似于Java中的instanceof关键字)。  

    fun getStringLength(obj: Any): Int? {
      if (obj is String) {
        // 做过类型判断以后，obj会被系统自动转换为String类型
        return obj.length 
      }

    //在这里还有一种方法，与Java中instanceof不同，使用!is
    // if (obj !is String){
    //   // XXX
    // }

    // 这里的obj仍然是Any类型的引用
    return null
    }
或者

    fun getStringLength(obj: Any): Int? {
      if (obj !is String)
        return null
      // 在这个分支中, `obj` 的类型会被自动转换为 `String`
      return obj.length
    }
甚至还可以

    fun getStringLength(obj: Any): Int? {
      // 在 `&&` 运算符的右侧, `obj` 的类型会被自动转换为 `String`
      if (obj is String && obj.length > 0)
        return obj.length
      return null
    }


### 区间:

区间表达式由具有操作符形式 .. 的 rangeTo 函数辅以 in 和 !in 形成。

区间是为任何可比较类型定义的，但对于整型原生类型，它有一个优化的实现。以下是使用区间的一些示例:

![](http://upload-images.jianshu.io/upload_images/9352581-a18309d9c8206b3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


送上新年福利：
![](http://upload-images.jianshu.io/upload_images/9352581-70230d57fe746ef7.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


好了上面对Kotlin基础的语法进行了大致的讲解，后面还会讲解关于Kotlin 的循环控制,条件控制，类，对象，接口，继承扩展等等的一条龙式的解说！大家晚安了！



