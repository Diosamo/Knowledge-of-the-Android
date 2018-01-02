## Kotlin 循环和条件控制（五）

上一篇我们讲了Kotlin的基础语法[Kotlin 实战语法（四）](https://www.jianshu.com/p/fbed6b999210) ,现在我们要开始学习循环和判断了 .

![](http://upload-images.jianshu.io/upload_images/9352581-bb414556f2b31524.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Kotlin 循环控制  

#### For循环:

for循环是最常见和古老的循环了,相信有一点编程基础的都知道for循环是学习大部分语言最先接触到的循环体,下面我们一起来解开它的面纱!

下面我用了一个数组和一个集合,我们使用不同的方式去使用for 循环做一些事情如下图:
![](http://upload-images.jianshu.io/upload_images/9352581-297eb2e876314898.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们使用了四种for 循环,前两种其实差不多,第一种其实就是个语法糖不用写大括号而已,那么后面两种呢,一种是循环的数组+.indices 这种可以让我们拿到索引,index就是索引了也就是0,1,2,3这种递增关系,通过array[index] 拿到值.最后一种呢?很简单就是值和索引一起拿,不过kotlin对这种方式做了优化不会产生额外的对象! 下面运行看一下运行的日志的输出:

![](http://upload-images.jianshu.io/upload_images/9352581-c536faa48359a46a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

哇,没有问题,和我们预期的结果是一样的,for循环简单吧,接下来是:
####  while 与 do...while 循环:

while 其实和我们汉语中的   "只要"   字很像,举个例子说明他们的区别,
      只要(我长到18岁了吗?){
            哇,今天我长了一岁!
      }
     // 这是 while 的意思,do...while 呢
     do{
             哇,今天我长了一岁!
      }
      只要(我长到十八岁了吗?)
其实do...While 和While 不同就在于do ... While 不管我现在是不是十八岁都会长!而While 是先看我已经18岁了吗?然后在进入循环体进行生长,所以是先判断后执行!
do while 是先执行后判断!  

模拟代码:


![](http://upload-images.jianshu.io/upload_images/9352581-13d687cf55e8126b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/9352581-4b504b4ef8e57347.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以看出do...while 在条件不满足的情况下还是执行了一次,而while并没有!

### 返回和跳转

Kotlin 有三种结构化跳转表达式和Java差不多,分别是 return , break , continue.

* return  默认从最直接包围它的函数或者匿名函数返回。
* break  终止最直接包围它的循环。
* continue  继续下一次最直接包围它的循环。

 ![](http://upload-images.jianshu.io/upload_images/9352581-39812d4078cd8534.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以看出当i为3的或3的倍数时没有print,跳过了进入下一次,当i>7 也就是等于8的时候会执行break,这个时候就跳出了循环也就没有打印后面的数字了,当然这是和Java类似的使用方式,那么kotlin 的特别之处在那里呢?

#### Break 和 Continue 标签
![](http://upload-images.jianshu.io/upload_images/9352581-afa26e67576f534b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上面我用了两个标签,loop2@ 和loop@ 也用了2次break,break 是直接跳出循环,当第一个判断满足时,就会跳出@loop指定的后面的内部的这个循环到下一次,然后下一次循环开始,当j=5时又跳出loop2@后面的最外层循环也就结束了!如果缓存continue就是继续下一次循环,但是原理一样!

总结来说:标签限制的 break 跳转到刚好位于该标签指定的循环后面的执行点。 continue 继续标签指定的循环的下一次迭代。

#### 在标签处返回
在 Kotlin 里本地函数和对象表达式、函数可以与函数常量一起嵌套。合法的 return 允许我们返回一个外部的函数。最重要的使用场景是从一个 lambda 表达式返回。记得我们写下这个的时候：

```
fun foo() {
  ints.forEach {
    if (it == 0) return
    print(it)
  }
}

```

这个 `return` 表达式从最近的封闭函数返回，也就是说 `foo`。（注意这样的无局部返回只支持 lambda 表达式传递给内联函数。如果我们需要从一个 lambda 表达式返回，我们就得标注它并合法地 `return`：

```
fun foo() {
  ints.forEach lit@ {
    if (it == 0) return@lit
    print(it)
  }
}

```

现在它只从 lambda 表达式返回。它常常更方便地使用隐式标签：这样的标签有和 lambda 传递的函数名相同的名字。

```
fun foo() {
  ints.forEach {
    if (it == 0) return@forEach
    print(it)
  }
}

```

另外，我们可以把 lambda 表达式换成一个匿名函数。位于匿名函数中的 `return` 指令将从匿名函数自身返回。

```
fun foo() {
  ints.forEach(fun(value: Int) {
    if (value == 0) return
    print(value)
  })
}

```

也就是说，当返回一个值时，解析器会给合法的返回以优先权。

```
return@a 1

```

意思是“标签 `@a` 返回 1 ”而不是“返回一个标签表达式 `@a 1`”。


### IF 表达式 

一个 if 语句包含一个布尔表达式和一条或多条语句。

![](http://upload-images.jianshu.io/upload_images/9352581-42a9f75f02e5ab5d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


在if 表达式中,if 和else 只允许有一个,else if 可以有多个,当然也可以只写 if ,else 和else if 都是根据情况去自己动态处理的!
还有if (a >= b) a else b 这种简洁的类似三元写法!


### 使用区间

使用 in 运算符来检测某个数字是否在指定区间内，区间格式为 x..y ：
实例


![](http://upload-images.jianshu.io/upload_images/9352581-b7bab6212d71e759.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这种两个数字中间两个点用通俗易懂的话来说就是从几到几,然后in 就是在不在的意思?什么代码的意思就是 x 在不在 1-10 区间里面,如果在就会输出x 在区间内!

### When 表达式

其实就是Java中的switch,给一个值根据代码中提供的不同值去执行不同的方案;
when 将它的参数和所有的分支条件顺序比较，直到某个分支满足条件。
when 既可以被当做表达式使用也可以被当做语句使用。如果它被当做表达式，符合条件的分支的值就是整个表达式的值，如果当做语句使用， 则忽略个别分支的值。
形式如下：

![](http://upload-images.jianshu.io/upload_images/9352581-c2118bd859131bf0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


我们可以看见When 特别的强大,可以他的扩展性,和选择性,而且使用场景都非常的给力,when可以对类型智能转换，你可以访问该类型的方法和属性而无需任何额外的检测,可以对传入的类型进行不同的判断,而且判断也支持函数,区间等很多语言无法做到的这种程度! 

![](http://upload-images.jianshu.io/upload_images/9352581-2a0db1a6db1646fb.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

写在后面:

到了今天大家已经学到Kotlin的很大一部分知识,但是别忘了即使回顾哦!十年磨一剑,相信Kotlin,相信未来!





    



