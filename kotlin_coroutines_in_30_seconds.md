# Kotlin 协程上手

Kotlin 协程（Coroutines）是一套异步编程（Asynchronous Programming）方案。开始编写协程代码之前有必要先认识协程具体用来解决什么问题，哪些场景适合用协程。从本质上理解它，让工具使用更加游刃有余。在 Kotlin 协程出现之前，Android 应用开发中，异步编程的工具已经有很多，如：Thread、Executor、Handler、AsyncTask、RxJava等。下面逐个分析这些工具：

直接使用 Thread 启动异步流程会使后台任务难以管理，线程得不到有效利用，通常以 Executor 取而代之，让 Executor 维护一个线程池，做到高效的线程调度。Handler 可以方便地将任务切换到主线程，属于专用化的场景需求，除此之外也可以用 HandlerThread 创建后台的 Handler，不过这样的场景大部分可以用 Executor 取代。AsyncTask 在设计上耦合数据和视图业务代码，已经被官方抛弃，不建议使用。RxJava 的底层多线程支持是 Executor 和 Handler，Kotlin 协程同样如此。如果在项目中自行实现多线程调度，那么可以直接使用 Executor 和 Handler。

基于 RxJava 开发的应用常常被冠名『函数响应式架构』，这样的应用天生具备可维护易扩展的特性，但很高的学习门槛和灵活的使用方式让开发者放弃了对它的探究，最终沦为只用于线程切换的工具。开发者会习惯性地将 Kotlin 协程和 RxJava 进行比较，因为它们适用的问题场景比较相似，并且都支持线程切换、避免回调地狱等。但它们的实现思路并不相同：RxJava 是基于观察者模式的流式开发，Kotlin 协程是基于状态模式的同步式编程。RxJava 历史已久、稳定而强大，去探索 RxJava 中的那些简便功能在新兴的 Kotlin 协程框架下如何实现远比论证孰优孰劣更有实践意义。

Android 开发中，异步编程的一个重要场景就是多线程编程。另外在主线程使用 Handler.post 执行代码也属于异步操作，尽管 post 之后的代码仍然是在主线程运行。异步调用的特点是函数调用栈不连续，也造成了代码追踪是跳跃式的。Kotlin 协程的厉害之处便是让开发者顺序书写异步代码，把肮脏的回调留给编译器去处理生成。

## 术语

协程（Coroutines）从字面上去抠它的意思是 Co-routines，协作程序。Kotlin 协程运行在线程之上，它是一段连续的程序代码却能够在多个线程间游走。

通过引入 Kotlin 官方提供的 `kotlinx.coroutines` 库，可以很方便地进行协程编程。接下来将逐步探讨这个库的用法，理解它为开发者制定的规则，从而正确、高效地进行协程编程。就好比写 RxJava 代码前，需理解它是一个事件驱动的响应式模型，开发者遵从 RxJava 的编程思想，把需求任务转化为事件模型，创建事件源、通过数个操作符将上游发送的事件转化为下游可接受的事件、末端操作触发事件开始传递。Kotlin 协程则是一个可挂起任务的协作模型，开发者将需求问题拆解成可挂起任务，编排任务的先后次序，最后启动协程让内部任务自动配合运作。

协程启动需要**协程域**（`CoroutineScope`），协程域可以约束协程的生存范围；一个域绑定着一个**协程上下文**（`CoroutineContext`），用于描述当前域的环境以及规定如何执行内部的协程。上下文可以包含多种子元素，如：**作业**（`Job`）、**调度器**（`CoroutineDispatcher`）、**协程名称**（`CoroutineName`）、**异常处理器**（`CoroutineExceptionHandler`）等。一个协程往往是协调多个子协程完成一个完整任务。当利用**协程构建函数**（Coroutine builders）从当前协程域启动新的协程时，这些新协程会自动和创建它的协程绑定主从关系，同时生成子域、子上下文。父子关系的连接支持着协程的**结构化并发**，父协程需要等待所有子协程结束才会结束，父协程的取消可以同时取消子协程，子协程异常可以上抛给父协程处理。

现在引入一个场景，使用 Github 的 [api](https://api.github.com/search/repositories?q=android&page=0&per_page=10&sort=forks) 构建一个请求 Github 仓库的网络应用，将理论结合到实际代码，认识协程的编码。

这个定制场景是在 Github 中搜索 `android` 关键词下的代码仓库，传统阻塞式基础设施代码如下：

```kotlin
fun call(page: Int): Repos {
  return repositoryRequest(page).run {
    InputStreamReader(URL(this).openStream())
  }.use {
    Gson().fromJson(it, Repos::class.java)
  }
}

private fun repositoryRequest(page: Int) =
  StringBuilder("https://api.github.com/search/repositories")
    .append("?q=").append("android")
    .append("&per_page=").append("25")
    .append("&sort=").append("forks")
    .append("&page=").append(page.toString())
    .toString()
```

`Repos` 是 api 响应数据的实体类（这里使用 [Gson](https://github.com/google/gson) 解析 JSON 数据）：

```kotlin
data class Repos(
  @SerializedName("total_count")
  val totalCount: Int,
  @SerializedName("incomplete_results")
  val incompleteResults: Boolean,
  @SerializedName("items")
  val items: List<Repo>
) {
  data class Repo(
    @SerializedName("name")
    val name: String,
    @SerializedName("owner")
    val owner: Owner,
    @SerializedName("description")
    val description: String,
    @SerializedName("forks")
    val forks: Int
  ) {
    data class Owner(
      @SerializedName("login")
      val name: String,
      @SerializedName("avatar_url")
      val avatarUrl: String,
      @SerializedName("url")
      val url: String
    )
  }
}
```

在获取到仓库列表后，下载仓库所有者的头像到本地目录：

```kotlin
fun download(url: String, name: String, dir: File): File {
  return File(dir, name).apply {
    URL(url).openStream().use { source ->
      outputStream().use { sink ->
        source.copyTo(sink)
      }
    }
  }
}
```

再次强调，以上代码均还未引入 Kotlin 协程的特性代码。

## Coroutine Builder

引入 Coroutines 库

```gradle
implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-core:1.4.3'
```

将阻塞代码转化为可挂起任务：

### `launch`

### `async/await`

### `withContext`

### `suspend` function

### Suspending vs Blocking

## CoroutineScope

### `coroutineScope`

### `supervisorScope`

## CoroutineContext

### `Job`

### `CoroutineDispatcher`

### `CoroutineExceptionHandler`

### `CoroutineName`
