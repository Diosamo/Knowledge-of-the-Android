## Rxjava2快速入门

### 写在前面:
RxJava的门槛相对应于其他技术是要高一点,想想自己以前第一次看完很大一篇文章的时候,也是三个字_很难受!但是现在我用RxJava很轻松,也很流畅,我相信大家通过不断的努力也是可以的,本文主要对API整理解释,大家还需要多使用,多练习,多领悟!

![](http://cniao5-imgs.qiniudn.com/o_1b10t250qn1ab2qb4st5p11fu9.jpg)

### RxJava 是什么?

    RxJava is a Java VM implementation of Reactive Extensions:
	a library for composing asynchronous and event-based programs by using observable sequences.
	(RxJava是Reactive Extensions的Java VM实现：一个通过使用可观察序列来编写异步和基于事件的程序的库。)

	It extends the observer pattern to support sequences of data/events and adds operators that allow you 
	to compose sequences together declaratively while abstracting away concerns about things like low-level 
	threading, synchronization, thread-safety and concurrent data structures.
	(它扩展了观察者模式以支持数据/事件序列，并添加了运算符，使您可以声明性地组合序列，同时抽象出对低级线程，同步，
	  线程安全性和并发数据结构等问题的关注。)

总结来说它是一个异步的响应式编程库,可以让你的代码逻辑更加简洁清晰,扩展性也更强,并且在线程间的调度,事件的处理上都具有十分的优雅性!

### Rx如何使用?
在这里我就直接开门见山去除那么多的文字描述用最直接的代码来告诉大家当然这里是快速入门,如果大家想要更加精细的学习本文后面会给大家推荐连接,大家可以去深入学习!好了,话已至此,我们开始吧!
下面用一张图表示RxJava最简单的运作
![关系图](https://ww3.sinaimg.cn/mw1024/52eb2279jw1f2rx46dspqj20gn04qaad.jpg)


1. 首先你需要创建一个上游对象Observable(被观察者)  

```java  
        Observable<Object> observable = Observable.create(new ObservableOnSubscribe<Object>() {
            @Override
            public void subscribe(ObservableEmitter<Object> e) throws Exception {
					
            }
        });
```



2. 然后你创建一个下游对象 Observer(观察者)

```java 
        Observer<Object> observer = new Observer<Object>() {
            @Override
            public void onSubscribe(Disposable d) {

            }

            @Override
            public void onNext(Object o) {

            }

            @Override
            public void onError(Throwable e) {

            }

            @Override
            public void onComplete() {

            }
        };
```

3.建立上下游关系  
	没错只需要下面这一行代码就可以  
	 observable.subscribe(observer);


### 实战

你已经学会使用最简单的Rxjava代码代码并且建立他们的关系,下面用同样的方式来写一段RxJava引以为傲的链式调用:

```java
 Observable
                .create(new ObservableOnSubscribe<Integer>() {
                    @Override
                    public void subscribe(ObservableEmitter<Integer> e) throws Exception {
                        e.onNext(1);
                        e.onNext(2);
                        e.onNext(3);
//                onComplete(); onError();   如果下游触发那么下游将收不到事件了
                        e.onNext(4);
                    }
                })
                .subscribe(new Observer<Integer>() {

                    private Disposable mDisposable;

                    @Override
                    public void onSubscribe(Disposable d) {
                        mDisposable = d; //用于切断上下游的通道
                    }

                    @Override
                    public void onNext(Integer o) {
                        if (o == 3) {
                            mDisposable.dispose();//切断通道   就收不到上游发出的事件了
                        }
                        Log.d(TAG, "onNext: "+o);

                    }

                    // 当事件处理中出现任何错误回调此方法后下游将收不到事件了
                    @Override
                    public void onError(Throwable e) {
                        Log.d(TAG, "onError: ");
                    }

                    // 当事件处理中回调此方法后下游将收不到事件了,可以自己手动调取次方法
                    @Override
                    public void onComplete() {
                        Log.d(TAG, "onComplete: ");
                    }
                });
```

### 线程调度:  
上面的代码是最基础的上游收发事件下游处理事件,大家可以仿照写一下自己,然后调试一下加深记忆,接下来要开始RxJava里面的线程调度了.  
在RxJava中, 已经内置了很多线程选项供我们选择, 例如有:  

Schedulers.io() 代表io操作的线程, 通常用于网络,读写文件等io密集型的操作   
Schedulers.computation() 代表CPU计算密集型的操作, 例如需要大量计算的操作  
Schedulers.newThread() 代表一个常规的新线程  
AndroidSchedulers.mainThread()  代表Android的主线程  

我们可以根据我执行代码的具体情况去指定所在的线程,我下面写一段指定线程的示列代码:

```java  
 observable.subscribeOn(Schedulers.newThread())   //指定obserable开启新线程执行的代码,第一次指定后以后在指定无效          
         .observeOn(AndroidSchedulers.mainThread()) 
         .observeOn(Schedulers.io())                //指定observer 在IO线程执行的代码,最后一次指定的线程才是observer运行的有效线程
         .subscribe(observer);
```

我们知道了subscruibeOn 是用来指定上游线程的,observeOn是用来指定接下来接受事件的代码运行的线程,那么在observable 和observe 之间还可以进行转换吗?比如我上游是将一群人的姓名加上666,然后最后打印出来,大家请看下面的代码:


```java  
 String[] names={" 张三"," 张二"," 张大",};      			//这群人的名字
            Observable.just(names)              		//将数组发送到下游
                    .subscribeOn(Schedulers.newThread()) //指定上游执行的线程new 一个新的线程
                    .observeOn(Schedulers.io())			//指定下面.map 操作符执行在io 线程
                    .map(new Function<String[], List<String>>() {   //执行给所有人的名字加上666再将集合传入下游
                        @Override
                        public List<String> apply(String[] strings) throws Exception {
                            ArrayList<String> newNames = new ArrayList<>();
                            for (String string : strings) {
                              newNames.add(string+"666");  
                            }
                            return newNames;
                        }
                    })
                    .observeOn(AndroidSchedulers.mainThread())  //指定下游执行的线程在主线程
                    .subscribe(new Consumer<List<String>>() {
                        @Override
                        public void accept(List<String> strings) throws Exception {
                            for (String name : strings) {
                                Log.d(TAG, "accept: "+name);     //接收到集合以后打印
                            }
                        }
                    });
```

### 操作符:  
上面的代码里面有一个.map 这个就是RxJava中的操作符,就是将上游发出的事件进行转换,可以转换成我们需要的东西在发送到下游去
常用的操作符有那些呢?

创建类操作符:

	create	是RxJava最基本的创建操作符了，直接使用即可.
	
	just	将对象转化为Observable对象，并且将其发射出去，可以使一个数字、一个字符串、数组、Iterate对象等，是一种非常快捷的创建Observable对象的方法
	
	from	操作符用来将某个对象转化为Observable对象，并且依次将其内容发射出去，from的接收值可以是集合或者数组，这个类似于just，但是just会将这个对象整个发射出去。比如说一个含有3个元素的集合，from会将集合分成3次发射，而使用just会发射一次来将整个的数组发射出去~
	
	defer	操作符只有当有Subscriber来订阅的时候才会创建一个新的Observable对象,也就是说每次订阅都会得到一个刚创建的最新的Observable对象，这可以确保Observable对象里的数据是最新的，而just则没有创建新的Observable对象，这样说可能并不利于大家消化，看下边与just对比示例~
	
	range	操作符根据输入的初始值【initial】和数量【number】发射number次、大于等于initial的值~
	
	Interval	所创建的Observable对象会从0开始，每隔固定的时间发射一个数字，需要注意的是这个对象是运行在computation Scheduler,所以要更新UI需要在主线程中进行订阅~
	
	Timer	会在指定时间后发射一个数字0，注意其也是运行在computation Scheduler~
	
	empty	创建一个Observable不发射任何数据、而是立即调用onCompleted方法终止~
	
	never	创建一个Observable不发射任何数据、也不给订阅ta的Observer发出任何通知~
	
	error	返回一个Observable，当有Observer订阅ta时直接调用Observer的onError方法终止
	
	Repeat	会将一个Observable对象重复发射，接收值是发射的次数，依然订阅在 computation Scheduler~
	
	delay	功能与timer操作符一样，但是delay用于在事件中，可以延迟发送事件中的某一次发送~

转换类操作符:

	Buffer	可以简单的理解为缓存，它可以批量或者按周期性从Observable收集数据到一个集合，然后把这些数据集合打包发射，而不是一次发射一个数据~

	FlatMap	扁平映射，作用是将一个原始Observable发射的数据进行变化，输出一个或多个Observable，然后将这些Observable发射的数据平坦化的放进一个单独的Observable（参数一般是Func1）~

	Map	映射，一般用于对原始的数据进行加工处理，返回一个加工过后的数据~
	
	GroupBy	用于对对象进行分组

	Sacn	sacn操作符是遍历源Observable产生的结果，通过自定义转换规则，依次输出结果给订阅者，

	Window	窗口，它可以批量或者按周期性从Observable收集数据到一个集合，然后把这些数据集合打包发射，而不是一次发射一个数据,类似于Buffer，但Buffer发射的是数据，Window发射的是Observable~


过滤类操作符:

	Debounce	debounce操作符在源Observable产品一个结果时开始计时，如果在规定的间隔时间内没有别的结果产生或者在此期间调用了onCompleted，则发射数据，否则忽略发射。

	Distinct	去重，过滤掉重复数据项~

	ElementAt	取值，取特定位置的数据项，索引是从0开始的~

	Filter	对发射的数据进行过滤，只发射符合条件的数据~

	First	首项，只发射首项或满足条件的首项数据~

	Last	末项，只发射末项或满足条件的末项数据~

	IgnoreElements	忽略所有数据，只保留终止通知(onError或onCompleted)~

	Sample	取样，定期扫描源Observable产生的数据，发射最新的数据~

	Skip	跳过前面的n项数据不进行处理~

	SkipLast	跳过后面的n项数据不进行处理~

	Take	与skip用法相反，保留前面的n项数据进行发射，而忽略后面的结果~

	TakeLast	与skipLast用法相反，只保留后面的n项数据进行发射，而忽略前面的结果~

组合类操作符:

	CombineLatest	当两个Observables中的任何一个发射了一个数据时，将两个Observables数据通过指定的规则进行处理，将结果进行发射~

	Join	无论何时，如果一个Observable发射了一个数据项，只要在另一个Observable发射的数据项定义的时间窗口内，就将两个Observable发射的数据合并发射~

	Merge	将两个Observable发射的数据按照时间顺序进行组合，合并成一个Observable进行发射~

	StartWith	在源Observable发射数据之前，先发射一个指定的数据序列或数据项~

	switchOnNext	把一组Observable转换成一个Observable，如果在同一个时间内产生两个或多个Observable产生的数据，只发射最后一个Observable产生的数据~
	
	Zip	使用一个指定的函数将多个Observable发射的数据组合在一起，然后将这个函数的结果作为单项数据发射，严格周期顺序进行合并，不能单独发射~


好了操作符在这里就简短快速的介绍完了,最终还是需要大家自己去多多练习实战就OK了.


Flowable与Observable

Flowable是RxJava2中的新成员， 同时旧的Observable也保留了。因为在 RxJava1.x 中，有很多事件不被能正确的背压，从而抛出MissingBackpressureException。

举个简单的例子，在 RxJava1.x 中的 observeOn， 因为是切换了消费者的线程，因此内部实现用队列存储事件。在 Android 中默认的 buffersize 大小是16，因此当消费比生产慢时， 队列中的数目积累到超过16个，就会抛出MissingBackpressureException， 初学者很难明白为什么会这样，使得学习曲线异常得陡峭。

而在 2.0 中，Observable 不再支持背压，而Flowable 支持非阻塞式的背压。并且规范要求，所有的操作符强制支持背压。幸运的是， Flowable 中的操作符大多与旧有的 Observable 类似。  

下面是使用Flowable的一段代码:

```java
 Flowable
                .create(new FlowableOnSubscribe<Object>() {
            @Override
            public void subscribe(FlowableEmitter<Object> e) throws Exception {

            }
        }, BackpressureStrategy.BUFFER)//这里指定Flowable 的背压策略
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new Subscriber<Object>() { //Flowable 配合Subscriber使用
                    @Override
                    public void onSubscribe(Subscription s) {  //这里和 Disposable 有一些不同 Subscription可以获取上游事件 和切断上下游
                        s.request(100);  //这里可以获取上游线程
                    }

                    @Override
                    public void onNext(Object o) {

                    }

                    @Override
                    public void onError(Throwable t) {

                    }

                    @Override
                    public void onComplete() {

                    }
                });
```

在Flowable的基础创建方法create中多了一个BackpressureStrategy类型的参数，
BackpressureStrategy是个枚举，源码如下：

	public enum BackpressureStrategy {
	   ERROR,BUFFER,DROP,LATEST,MISSING
	}
Flowable的异步缓存池不同于Observable，Observable的异步缓存池没有大小限制，可以无限制向里添加数据，直至OOM,而Flowable的异步缓存池有个固定容量，其大小为128。
BackpressureStrategy的作用便是用来设置Flowable通过异步缓存池存储数据的策略。

	ERROR	在此策略下，如果放入Flowable的异步缓存池中的数据超限了，则会抛出MissingBackpressureException异常。

	DROP	在此策略下，如果Flowable的异步缓存池满了，会丢掉将要放入缓存池中的数据。

	LATEST	与Drop策略一样，如果缓存池满了，会丢掉将要放入缓存池中的数据，不同的是，不管缓存池的状态如何，LATEST都会将最后一条数据强行放入缓存池中。

	BUFFER	此策略下，Flowable的异步缓存池同Observable的一样，没有固定大小，可以无限制向里添加数据，不会抛出MissingBackpressureException异常，但会导致OOM。

	MISSING	此策略表示，通过Create方法创建的Flowable没有指定背压策略，不会对通过OnNext发射的数据做缓存或丢弃处理，需要下游通过背压操作符（onBackpressureBuffer()/onBackpressureDrop()/onBackpressureLatest()）指定背压策略。

onBackpressureXXX背压操作符

Flowable除了通过create创建的时候指定背压策略，也可以在通过其它创建操作符just，fromArray等创建后通过背压操作符指定背压策略。
onBackpressureBuffer()对应BackpressureStrategy.BUFFER
onBackpressureDrop()对应BackpressureStrategy.DROP
onBackpressureLatest()对应BackpressureStrategy.LATEST


### 总结:

RxJava 学习的路比较漫长,小伙伴们还需要多多加油,这里只是快速的介绍了一些RxJava中的常用的一些知识,在这里给大家推荐几个RxJava相关文章连接:  
[给初学者的RxJava教程](https://juejin.im/user/573dba2171cfe448aa97b7b0)  
[给 Android 开发者的 RxJava 详解](http://gank.io/post/560e15be2dca930e00da1083)  
[RxJava Doc](http://reactivex.io/RxJava/2.x/javadoc/)  
[RxAndroid](https://github.com/ReactiveX/RxAndroid)   
[RxJava](https://github.com/ReactiveX/RxJava) 


![me](http://static.codeceo.com/images/2014/07/programmer-and-whore.jpg)

好了我要出去了,大家加油　　[如有更好的建议提议,可以发到我的邮箱diosamolee2014@gmail.com](#)