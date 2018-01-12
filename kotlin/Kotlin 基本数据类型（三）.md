### Kotlin 基本数据类型（三） 

上一次大家学会了创建你的第一个Kotlin应用 [Kotlin 快速创建您的第一个应用（二）](https://www.jianshu.com/p/1157f481c32a) 

![](http://upload-images.jianshu.io/upload_images/9352581-46774378e7103718.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### Kotlin 基本数据类型：  

Kotlin 的基本数值类型包括 Byte、Short、Int、Long、Float、Double 等。不同于Java的是，字符不属于数值类型，是一个独立的数据类型。

    类型	      位宽度         字节对应
    Double	       64            8个字节
    Float	       32            4个字节
    Long	       64            8个字节
    Int	           32            4个字节
    Short	       16            2个字节
    Byte	       8             1个字节

### 字面常量： 

下面是所有类型的字面常量：

* 十进制：123
* 长整型以大写的 L 结尾：123L
* 16 进制以 0x 开头：0x0F
* 2 进制以 0b 开头：0b00001011
* 注意：8进制不支持

Kotlin 同时也支持传统符号表示的浮点数值：

* Doubles 默认写法: 123.5, 123.5e10
* Floats 使用 f 或者 F 后缀：123.5f

你可以使用下划线使数字常量更易读：

        val oneMillion = 1_000_000
        val creditCardNumber = 1234_5678_9012_3456L
        val socialSecurityNumber = 999_99_9999L
        val hexBytes = 0xFF_EC_DE_5E
        val bytes = 0b11010010_01101001_10010100_10010010

### 类型的比较：

Kotlin 中没有基础数据类型，只有封装的数字类型，你每定义的一个变量，其实 Kotlin 帮你封装了一个对象，这样可以保证不会出现空指针。数字类型也一样，所有在比较两个数字的时候，就有比较数据大小和比较两个对象是否相同的区别了。

在 Kotlin 中，三个等号 === 表示比较对象地址，两个 == 表示比较两个值大小。不同类型能不能比较呢？ 当然是不能拉，不过类型是可以转换的后面会说.

![](http://upload-images.jianshu.io/upload_images/9352581-3dc473b6decf7a4a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 类型转换:

由于不同的表示方式，较小类型并不是较大类型的子类型，较小的类型不能隐式转换为较大的类型。 这意味着在不进行显式转换的情况下我们不能把 Byte 型值赋给一个 Int 变量。  

![](http://upload-images.jianshu.io/upload_images/9352581-5ae01dd39a889207.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们可以代用其toInt()方法。

![](http://upload-images.jianshu.io/upload_images/9352581-5e7a97bf303f4379.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

每种数据类型都有下面的这些方法，可以转化为其它的类型：

        toByte(): Byte
        toShort(): Short
        toInt(): Int
        toLong(): Long
        toFloat(): Float
        toDouble(): Double
        toChar(): Char

有些情况下也是可以使用自动类型转化的，前提是可以根据上下文环境推断出正确的数据类型而且数学操作符会做相应的重载。例如下面是正确的：
      
 ![](http://upload-images.jianshu.io/upload_images/9352581-49d4f37e21e7cd5a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 位操作符: 

对于Int和Long类型，还有一系列的位操作符可以使用，分别是：

![](http://upload-images.jianshu.io/upload_images/9352581-59767e21dbd3275b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

    shl(bits) – 左移位 (Java’s <<)
    shr(bits) – 右移位 (Java’s >>)
    ushr(bits) – 无符号右移位 (Java’s >>>)
    and(bits) – 与
    or(bits) – 或
    xor(bits) – 异或
    inv() – 反向

### 字符   
和 Java 不一样，Kotlin 中的 Char 不能直接和数字操作，Char 必需是单引号''包含起来的。比如普通字符 '0'，'a'。

![](http://upload-images.jianshu.io/upload_images/9352581-e14dbeca3d0becac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

字符字面值用单引号括起来: '1'。 特殊字符可以用反斜杠转义。 支持这几个转义序列：\t、 \b、\n、\r、\'、\"、\\ 和 \$。 编码其他字符要用 Unicode 转义序列语法：'\uFF00'。

我们可以显式把字符转换为 Int 数字：  

    fun decimalDigitValue(c: Char): Int {
        if (c !in '0'..'9')
            throw IllegalArgumentException("Out of range")
        return c.toInt() - '0'.toInt() // 显式转换为数字
    }

当需要可空引用时，像数字、字符会被装箱。装箱操作不会保留同一性。


### 布尔

布尔用 Boolean 类型表示，它有两个值：true 和 false。

若需要可空引用布尔会被装箱。

内置的布尔运算有：

    ||     短路逻辑或
    &&    短路逻辑与
    !    逻辑非

### 数组 

数组用类 Array 实现，并且还有一个 size 属性及 get 和 set 方法，由于使用 [] 重载了 get 和 set 方法，所以我们可以通过下标很方便的获取或者设置数组对应位置的值。

数组的创建多种方式：可以是使用函数arrayOf()；也可以是使用工厂函数,还可以创建空数组，只读，还可以创建指定长度的可空数组，如下所示，我们分别创建了不同 的数组：
![](http://upload-images.jianshu.io/upload_images/9352581-2c841fe951413ac5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 字符串 

和 Java 一样，String 是可不变的。方括号 [] 语法可以很方便的获取字符串中的某个字符，也可以通过 for 循环来遍历：

    for (c in str) {
        println(c)
    }


Kotlin 支持三个引号 """ 扩起来的字符串，支持多行字符串，比如：

![](http://upload-images.jianshu.io/upload_images/9352581-63e0e856eaa97542.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

当然这种输出可能会有一些前置空格，不过我们可以通过String 通过 trimMargin() 方法来删除多余的空白。

![](http://upload-images.jianshu.io/upload_images/9352581-50c6cc6144d134a4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)   

默认 | 用作边界前缀，但你可以选择其他字符并作为参数传入，比如 trimMargin(">")。

![我从小就爱学习](http://upload-images.jianshu.io/upload_images/9352581-e904c3e967332a92.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 写在后面：
 今天我们学习完了Kotlin 的基本数据类型，下一篇我们讲Kotlin的语法，今天是2018第一天，元气满满祝大家今年登上高峰！Goodbye！
