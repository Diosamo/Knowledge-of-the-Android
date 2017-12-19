# Retrofit2快速入门

![](http://5b0988e595225.cdn.sohucs.com/images/20171013/de9d5270d42047c0800e79d53d5b3042.jpeg)


大家好,又是心情澎湃的一天,今天我将给大家介绍Retrofit2这个库.


### Retrofit2是什么?

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
* **请求方法类**  

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

[Retrofit官方文档](https://square.github.io/retrofit/)













(未完待续)