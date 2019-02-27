# 前言
RxJS是一套库，用于解决WEB编程中越来越多的异步操作以及许多不同的异步API写法带来的一些麻烦。
这些问题主要出现在以下几种情况：
 - 竞态条件 (Race Condition)：比如你用异步操作更新了一个资源，然后又发送另一个操作去获取这个资源，就可能获取到还没有更新完成的资源。
 - 内存泄露（Memory Leak)：我们如今更常写的SPA单面应用，在切换页面的时候，很可能会出现已经无用的绑定未解除，这样资源得不到及时的释放。
 - 复杂的状态 (Complex State)：这个很好理解，一旦有了异步操作，所有的状态可能会变得很复杂。- 异常的处理 (Exception Handling)：想要自如地捕捉异步状况下的异常，是一件比较困难的事情。

# 重要元素
**一个核心——Observable + Operators(map, filter...)**
**三个重点——Observer、Subject、Schedulers**

# Observable
## 观察者模式&迭代器模式
Observable就像是这两种模式思想的结合，Observable具备生产者推送资料的特性，同时拥有序列处理资料的方法(map, filter...)。Observable 可以同时处理同步跟非同步行为。

## Observer观察者
Observable可以被订阅/被观察，订阅Observable 的就是观察者(Observer)。观察者是一个具有三个方法(method)的对象，每当Observable发生事件时，便会呼叫观察者相对应的方法。订阅一个 Observable 就像在执行一个 function。

观察者拥有三个方法：
- next：每当 Observable 发送出新的值，next 方法就会被呼叫。
- complete：在 Observable 没有其他的资料可以取得时，complete 方法就会被呼叫，在 complete 被呼叫之后，next 方法就不会再起作用。
- error：每当 Observable 内发生错误时，error 方法就会被呼叫。

## 创立Observable实例的方法
- create
- of
- from
- fromEvent
- fromPromise
- never
- empty
- throw
- interval
- timer

## Observable拥有的方法
- take：取前几个元素后就结束。
- first：取 observable 送出的第 1 个元素之后就直接结束，行为跟 take(1) 。
- takeUntil：在某件事情发生时，让一个 observable 直送出 完成(complete)讯息。
- concatAll：有时我们的 Observable 送出的元素又是一个 observable，就像是二维阵列，阵列裡面的元素是阵列，这时我们就可以用 concatAll 把它摊平成一维阵列，大家也可以直接把 concatAll想成把所有元素 concat 起来。 
- skip：略过前几个送出元素的 。
- takeLast：倒过来取最后几个。
- last：takeLast(1) 的简化写法。
- concat：多个 observable 实例合併成一个。
- startWith：observable 的一开始塞要发送的元素。
- merge ：合併 observable。
- combineLatest：取得各个 observable 最后送出的值，再输出成一个值。
- withLatestFrom：跟 combineLatest 有点像，只是他有主从的关系，只有在主要的 observable 送出新的值时，才会执行 callback，附随的 observable 只是在背景下运作。
- zip：取每个 observable 相同顺位的元素并传入 callback，也就是说每个 observable 的第 n 个元素会一起被传入 callback。

