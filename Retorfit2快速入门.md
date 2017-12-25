# Retrofit2快速入门

![](http://5b0988e595225.cdn.sohucs.com/images/20171013/de9d5270d42047c0800e79d53d5b3042.jpeg)


大家好,又是心情澎湃的一天,今天我将给大家介绍Retrofit2这个库.


### Retrofit2是什么?

Retrofit是由Square公司出品的针对于Android和Java的类型安全的Http客户端，吸取了RESTful的风格,实质上就是对okhttp 进行了封装,利用动态代理实现了网络接口底层请求,然后将返回的数据就行转换成我们指定的Bean对象,极大的提高了效率,和网络体验.

[RESTful相关文档](https://github.com/Diosamo/Knowledge-of-the-Android/blob/master/RESTful%E6%98%AF%E4%BB%80%E4%B9%88.md)

### 使用依赖
首先在**build.gradle**中添加如下代码，添加Retrofit2库

	
	compile 'com.squareup.retrofit2:retrofit:2.3.0'

### 创建实列
```java
	Retrofit retrofit = new Retrofit.Builder()
        .baseUrl("baseurl/") //这里填入端口的url   
        .build();
```

必须以 /（斜线） 结束，不然会抛出一个IllegalArgumentException,所以如果你看到别的教程没有以 / 结束，那么可能是直接从Retrofit1 copy过来的。

### 定义接口

以获取一本书的页数为例子
```java
public interface API {
    @GET("book/{page}")
    Call<ResponseBody> getPage(@Path("page") int id);
}
```
在通过上面构建的实列对象retorfit 进行下一步操作
	API api = retrofit.create(API.class);

构建出代理对象.


### 开始请求

上一部已经拿到了代理对象,接下来我们就需要使用代理对象来进行网络请求获取数据,如下代码:

```java
	Call<ResponseBody> page = api.getPage(10);

        page.enqueue(new Callback<ResponseBody>() {
            @Override
            public void onResponse(Call<ResponseBody> call, Response<ResponseBody> response) {
				//请求成功返回的数据                

            }

            @Override
            public void onFailure(Call<ResponseBody> call, Throwable t) {
				//请求失败

            }
        });
```

当然上面只是异步的请求,回调到这两个方法如果使用同步请求:
```java
 	try {
            Response<ResponseBody> response = page.execute();
            //可以根据返回的response在做处理
        } catch (IOException e) {
            e.printStackTrace();
        }
```

注意同步请求不要在主线程去使用,一半是在子线程里面发起请求,后面的代码需要同步返回的数据方才使用
当你将一些异步请求压入队列后，甚至你在执行同步请求的时候，你可以随时调用 cancel 方法来取消请求

## Retrofit注解详解

刚刚已经完成了retrofit最基本的快速使用方法,那么接下来就详细介绍一下retrofit的注解,retrofit里面有很多注解,是一个很轻量级的库,
一共37个类就有22个是注解类,所以大家这一块一定要仔细认真的看一下.  

*  **请求方法类**  

@PATCH、@OPTIONS、@HTTP、@HEAD、@PUT、@GET、@PUT、@DELETE
方法注解和RESTFUL API有关   
@PUT，PUT方法用来创建一个URI已知的资源，或对已知资源进行完全替换，比如users/1，因此PUT方法一般会用来更新一个已知资源，
除非在创建前，你完全知道自己要创建的对象的URI。    
@PATCH ，PATCH方法是新引入的，是对PUT方法的补充，用来对已知资源进行局部更新  
@HEAD ，与参数注解@Header不同，只请求页面的首部。  
@OPTIONS 允许客户端查看服务器的性能  
@HTTP ,使用用户自定义的verb进行网络请求	  



* **标记类**
@FormUrlEncoded、@Multipart、@Streaming。  

@FormUrlEncoded	请求体是 From 表单  
@Multipart	请求体是支持文件上传的 From 表单  
@Streaming	响应体的数据用流的形式返回  



* **参数类**  
@Headers、@Header、@Body、@Field、@FieldMap、@Part、@PartMap@、Path、@Query、@QueryMap、@Url

@Headers:使用 @Headers 注解设置固定的请求头，所有请求头不会相互覆盖，即使名字相同。  

@Header: 使用 @Header 注解动态更新请求头，匹配的参数必须提供给 @Header ，若参数值为 null ，这个头会被省略，否则，会使用参数值的 toString 方法的返回值。

@Body: 使用 @Body 注解，指定一个对象作为 request body 。

@Field: 表单提交，如登录

@FieldMap 、@Part 、@PartMap 、@Path: 请求 URL 可以替换模块来动态改变，替换模块是 {}包含的字母数字字符串，替换的参数必须使用 @Path 注解的相同字符串。

@Query: 查询参数

@QueryMap: 复杂的查询参数

@Url: 作用于方法参数,用于添加请求的接口地址


### Bean对象转换
要自定义Converter<F, T>，需要先看一下GsonConverterFactory的实现，
GsonConverterFactory实现了内部类Converter.Factory。

其中GsonConverterFactory中的主要两个方法，主要用于解析request和response的，
在Factory中还有一个方法stringConverter，用于String的转换。

引入Gson支持:  

	compile 'com.squareup.retrofit2:converter-gson:2.0.2'
通过GsonConverterFactory为Retrofit添加Gson支持：  

```java  
Gson gson = new GsonBuilder()
      //配置你的Gson
      .setDateFormat("yyyy-MM-dd hh:mm:ss")
      .create();

Retrofit retrofit = new Retrofit.Builder()
      .baseUrl("http://localhost:4567/")
      //可以接收自定义的Gson，当然也可以不传
      .addConverterFactory(GsonConverterFactory.create(gson))
      .build();   

```

然后通过  Call<ResponseBody> 这里替换ResponseBody 为自己的Bean对象Call<JavaBean> 然后请求回来的数据就会自动转换.

### 结合okhttp,并使用Interceptor  
对应依赖:

		compile 'com.squareup.okhttp3:logging-interceptor:3.5.0'

		testImplementation 'com.squareup.okhttp3:mockwebserver:3.9.1'

Retrofit 2.0 底层依赖于okHttp，所以需要使用okHttp的Interceptors 来对所有请求进行拦截。
我们可以通过自定义Interceptor来实现很多操作,打印日志,缓存,重试等等。

要实现自己的拦截器需要有以下步骤

	//创建OkHttpClient
OkHttpClient client = new OkHttpClient.Builder()
                .addInterceptor(new HttpLoggingInterceptor())
                .build();
retrofit = new Retrofit.Builder()
        .baseUrl(Urls.baseUrl)
        .client(client)//添加自定义OkHttpClient
        .build();

### 如何结合RxJava

引入RxJava支持:

	//这里支持的是RxJava2
	compile 'com.squareup.retrofit2:adapter-rxjava2:2.3.0'
	compile "io.reactivex.rxjava2:rxjava:2.1.7"

如何添加:  
```java
retrofit = new Retrofit.Builder()
        .baseUrl(Urls.baseUrl)
 		// 针对rxjava2.x  
		.addCallAdapterFactory(RxJava2CallAdapterFactory.create())
        .build();
```  

在请求的接口中直接指定Observable 的Rxjava对象:  

	public interface Api{
	  @POST("/page")
	  Observable<Event1> getBook();
	}

然后在通过以下代码完成一套行云流水的结合操作:  

```java   
 Retrofit retrofit= new Retrofit.Builder()
                .baseUrl(baseUrl)
                .addConverterFactory(GsonConverterFactory.create())
                .addCallAdapterFactory(RxJavaCallAdapterFactory.create())
                .build();

        API movieService = retrofit.create(API.class);

        movieService.getTest()
                .subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new Subscriber<Event1>() {
                    @Override
                    public void onCompleted() {
                    }

                    @Override
                    public void onError(Throwable e) {
                    }

                    @Override
                    public void onNext(MovieEntity movieEntity) {
                    }
                });

```   

这样完成了Retrofit和Rxjava的结合,这只是最基本的操作,更多操作还需要大家多多练习,提升自己,方能想怎么玩就怎么玩!
这是官方文档,想要深入研究的小伙伴可以好好学一波,加油!  

[Retrofit官方文档](https://square.github.io/retrofit/)  


 ![](http://upload-images.jianshu.io/upload_images/9352581-0099c4e4bca81c76.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
[如有更好的建议提议,可以发到我的邮箱diosamolee2014@gmail.com](#)