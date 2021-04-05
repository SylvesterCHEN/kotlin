# Kotlin 协程上手

Kotlin Coroutines 是一套异步编程方案。开发者习惯性地将 Kotlin 协程和 RxJava 进行比较，如它们都支持线程切换、避免回调地狱。但它们的实现思路并不相同：RxJava 是基于观察者模式的流式开发，Kotlin 协程是基于状态模式的同步式编程。RxJava 历史已久、稳定而强大，所以去探索 RxJava 中的功能在新兴的 Kotlin 协程框架下如何实现显然比论证孰优孰劣更有实践意义。

Kotlin 协程是一段可以在多个线程间游走的子程序。

## 术语

### CoroutineScope

### CoroutineContext

### Coroutine Builder

### Job

### Dispatcher
