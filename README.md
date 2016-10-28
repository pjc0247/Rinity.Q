Rinity.Q
====

Basic Usage
----
```cs
Q.Defer(() => {
    Console.WriteLine("after 1 sec, on main thread");
}, 1000);

Q.Async(() => {
    Console.WriteLine("after 1 sec, on therad pool");
}, 1000);
```

ContinueWith
----
```cs
Q.Defer(() => { /* 1 */ })
    .ContinueWith(() => { /* 2 */ })
    .ContinueWith(() => { /* 3 */ });
```

Advanced Options
----
__TargetThread__<br>
* Any
    * __Q__가 알아서 적절한 스레드에 배분합니다. 대부분의 케이스에 `SameThread`와 같이 동작합니다.
* SameThread
    * 이어지는 작업이 이전 작업과 같은 스레드에서 시작합니다.
* ThreadPool
    * 이어지는 작업이 무조건 스레드 풀에서 시작합니다.
* MainThread
    * 이어지는 작업이 무조건 메인 스레드에서 시작합니다.


__TaskOption__<br>
태스크에 대한 힌트를 제공합니다. 이러한 힌트는 __Q__가 작업을 알맞게 배분하는데 도움을 줄 수 있습니다.

* LightTask
    * 가벼운 작업
* LongRunning
    * 아주 오래 걸리는 작업

```cs
QTask.Create(
    () => {},
    QTargetThread.SameThread,
    QTaskOption.LongRunning);

Q.Async(() => { /* 1 */ })
    .ContinueWith(() => { /* 2 */ }, QTargetThread.MainThread);
```
