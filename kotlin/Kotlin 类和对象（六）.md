## Kotlin 类和对象（六）   

上一篇我们讲了Kotlin的循环还有条件控制[Kotlin 循环和条件控制（五）](https://www.jianshu.com/p/1667609e7e5b) ,这次我们将要学习一个Kotlin的类与对象.

![](http://upload-images.jianshu.io/upload_images/9352581-040f4986b8cdcb9e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 类:

Kotlin 中的类使用的也是 class 关键字声明,类由类名、类头（指定它的类型参数、主构造器等等）和类体组成，用花括号包围。类头和类体都是可选的；如果类没有类体则花括号可以省略。

    //有类体的类
    class Test {
  
     }
    
    //没有类体的类
    class Test

### 构造器:

构造器?

构造器是干哈的?

小白可能会很懵逼啊,是的构造器是用来初始化一个类的,比如我这个类是沸腾的白开水,我需要使用它,我怎么才能拥有它呢?

    1.直接用锅煮.
    2.用热水壶.
    3.用太阳晒

有的同学可能说这是不同的方式去成功拿到开水啊,是的构造器也是这样,我们的类可以有多个构造,如果你不写,也是有的!只是隐藏了起来,以免大家看见太多代码头晕!好了下面我来细致解释一下各种构造器,以及各做方式去初始化一个类:

这里有4个类,他们什么都没有,但是他们都是有构造的,并且是一样的构造,只是我们的写法可以去省略这些代码

![](http://upload-images.jianshu.io/upload_images/9352581-fd08f7768e7500c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这里的constructor 是他们省略的一个构造,所以记住一句话,只要是类就有构造!


![](http://upload-images.jianshu.io/upload_images/9352581-6a969050aaa976e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果构造函数有注解或可见性修饰符，这个 constructor 关键字是必需的，并且这些修饰符在它前面,像下面这种写在类名旁边的构造就是这个类的主构造,可以传递不同的内容去初始化这个类.当然直接指定var,val这种参数可以让这个参数变成这个类的成员,在类中使用

![](http://upload-images.jianshu.io/upload_images/9352581-751df77af491b670.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

主构造函数不能包含任何的代码。初始化的代码可以放到以 init 关键字作为前缀的初始化块（initializer blocks）中。

![](http://upload-images.jianshu.io/upload_images/9352581-b33085ad98cff61c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


当然有主就有次,次构造呢就是我之前举得例子那样,有很多种方式,比如用太阳把水晒沸腾...
开个玩笑哦,继续看:


![](http://upload-images.jianshu.io/upload_images/9352581-915f11ce379a6ffe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这里我就给Dad1 这个类写了一个不同的构造,主构造是一个空的,而次构造需要一个String类型的name来初始化这个类,每个次构造函数需要委托给主构造函数， 可以直接委托或者通过别的次构造函数间接委托。委托到同一个类的另一个构造函数用 this 关键字即可,那么怎去委托同一个类的其他构造呢?请看第三个次构造,第三个次构造就是通过传入2个参数去委托第二个构造,最后在委托回主构造.


如果你不希望你的类有一个公有构造函数，你需要声明一个带有非默认可见性的空的主构造函数：

![](http://upload-images.jianshu.io/upload_images/9352581-c8f4877bba5a3c3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

还有一种直接给构造中参数复制的操作,在继承中可以发挥一些用途,其他的恕我还没有探索到...

![](http://upload-images.jianshu.io/upload_images/9352581-3dde54221b8dfc55.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 创建类的实例   

在Kotlin里面创建实列和Java不一样,变得更加简单直接像调用函数一样,创建,注意:  不用使用new了! 不用使用new了! 不用使用new了!

![](http://upload-images.jianshu.io/upload_images/9352581-7c892842ba48105a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

创建嵌套类、内部类和匿名内部类的类实例在[嵌套类]我们下一篇再讲。

### 继承  

在Kotlin中有一个共同超类,也就是Java中的Object ,在Kotlin 里面加Any,但是Any类中只有equals()、hashCode()和toString() 三个函数外没有其他任何成员了.

怎么去继承一个类呢?

很简单就是使用: 你要继承的类,在父类前面加上open,这里的open 其实就是指可以被继承,Kotlin 里面所有的类默认是final ,需要继承的类就指定open,并且需要指定构造,就是下面的箭头所指的构造去初始化父类.

![](http://upload-images.jianshu.io/upload_images/9352581-ea5f8e24d5c74777.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

淡然也可以通过关键字super去初始化父类

![](http://upload-images.jianshu.io/upload_images/9352581-a21306dcb9e38665.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

覆盖方法与属性

覆盖方法和属性需要加上 override 这个关键字 , 如果不想子类覆盖就在前面指定 final 这样子类就没办法覆盖了.不仅可以在成员位置覆盖,在主构造覆盖也是可以的.

![](http://upload-images.jianshu.io/upload_images/9352581-201eec443d23c477.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 调用超类实现

派生类中的代码可以使用 *super* 关键字调用其超类的函数与属性访问器的实现：  

```
open class Foo {
    open fun f() { println("Foo.f()") }
    open val x: Int get() = 1
}

class Bar : Foo() {
    override fun f() { 
        super.f()
        println("Bar.f()") 
    }

    override val x: Int get() = super.x + 1
}

```

在一个内部类中访问外部类的超类，可以通过由外部类名限定的 *super* 关键字来实现：`super@Outer`：  

```
class Bar : Foo() {
    override fun f() { /* …… */ }
    override val x: Int get() = 0

    inner class Baz {
        fun g() {
            super@Bar.f() // 调用 Foo 实现的 f()
            println(super@Bar.x) // 使用 Foo 实现的 x 的 getter
        }
    }
}
```
### 覆盖规则   

在 Kotlin 中，实现继承由下述规则规定：如果一个类从它的直接超类继承相同成员的多个实现， 它必须覆盖这个成员并提供其自己的实现（也许用继承来的其中之一）。 为了表示采用从哪个超类型继承的实现，我们使用由尖括号中超类型名限定的 *super*，如 `super<Base>`：

```
open class A {
    open fun f() { print("A") }
    fun a() { print("a") }
}

interface B {
    fun f() { print("B") } // 接口成员默认就是“open”的
    fun b() { print("b") }
}

class C() : A(), B {
    // 编译器要求覆盖 f()：
    override fun f() {
        super<A>.f() // 调用 A.f()
        super<B>.f() // 调用 B.f()
  }
}

```

同时继承 `A` 和 `B` 没问题，并且 `a()` 和 `b()` 也没问题因为 `C` 只继承了每个函数的一个实现。 但是 `f()` 由 `C`继承了两个实现，所以我们**必须**在 `C` 中覆盖 `f()` 并且提供我们自己的实现来消除歧义。

###  抽象类  

类和其中的某些成员可以声明为 *abstract*。 抽象成员在本类中可以不用实现。 需要注意的是，我们并不需要用 `open` 标注一个抽象类或者函数——因为这不言而喻。

我们可以用一个抽象成员覆盖一个非抽象的开放成员

```
open class Base {
    open fun f() {}
}

abstract class Derived : Base() {
    override abstract fun f()
}

```


![](http://upload-images.jianshu.io/upload_images/9352581-fb9e1e98a14b972a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### 总结: 

Kotlin的类和对象是最基础的东西,也是对于小白入门比较困难的东西,大家多多理解,理解是最重要的,加油!












