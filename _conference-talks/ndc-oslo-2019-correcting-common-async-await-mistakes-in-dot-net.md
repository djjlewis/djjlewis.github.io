---
layout: post
conference: NDC Oslo 2019
title: Correcting Common Async/Await Mistakes in .NET
speaker: Brandon Minnick
date: 2019-07-10
link: https://www.youtube.com/watch?v=J0mcYVxJEl0
youtube-id: J0mcYVxJEl0

---

 <iframe width="640" height="360" src="https://www.youtube.com/embed/{{ page.youtube-id }}"></iframe> 

## Introduction

.NET includes a managed thread pool. This includes a syncronisation context that is responsible for orchestrating
threads e.g. starting / stopping threads

Different hardware will have different amounts of threads available and is dependent on the amount of virtual memory

Async /  Await keywords: Adding the async keywork to a method will cause the compiler to create a class which will be a
state machine for your method. It will convert any local variables to fields, private or public if it is a paramter. The
variable names will be renamed slightly by the compiler in order to avoid naming collisions.

The state machine class will inherit from IAsyncStateMachine. This interface includes a MoveNext() method which most
people will be used to seeing whenever an stack trace is shown for an exception that occurred in async code.

The state machine will have n+1 swtich cases where n is the number of await calls. 

For each case, it will assign the awaiter of an async task to a variavle, increment the counter by 1, then return back
to the calling thread.

MoveNext wraps the method inside a Try/Catch block. Any exception in your code will be caught and rethrown. Some async
methods are "fire and forget" like Task.Run. If you put some code in here then your exception will be swallowed.

14:00

16:40

Never ever ever ever use .Wait(). .Wait() will always cause the current thread to block. It will also create another
thread to run the code before .Wait which is not needed. Instead of .Wait just use the await keyword.

If you do need to run syncronous code, use GetAwaiter().GetResult(); instead. It's better than .Wait because .Wait
throws an Aggregate exception whereas GetResult will return the original exception.

## ConfigureAwait(false)

in UI where there is a sycnronisation context, if code is called via await, then we can use ConfigureAwait(false) this
tells the syncronisation context that the rest of the method code after the await keyword can be run on any thread and
does not need to return to the UI thread. This is beneficial because we should keep the UI thread as free as possible to
run UI related processing.


## Return a task directly when you can

In some methods, if the only thing done is await, then we can return the task immediately without needing the async and
await keywords. This saves a context switch so a new thread isn't created and also means the IAsyncStateMachine isn't
generated so saves on a bit of perf and memory overhead (100 bytes!)

If the method is wrapped in a try/catch , we should use async await otherwise the catch will never run.

## Value task

use value task when you return the hot path in a method. ValueTask is a value type so lives in a stack

Should use value task if the hot path in your async method does not use await keyword.

## async void

If you need to call an async method from your constructor, use an async void method

almost impssoble to catch an exception in an async void method as the code is executed in a background thread and we
can't await 

async void is not recommended because very difficult know it is async just looking at the call and can introduce bugs
and possible race conditions ad the async void method will run at the same the rest of the method continues.

## safe fire and forget

custom class called SafeFireAndForget that can configure await, and pass an Action for OnException that will get called
if an exception happens.

## AsyncCommand

in MVVM / xamarin command takes an Action which is void, so if it is async it will be an async void method. Speaker has
a custom library called AsyncCommand which will wrap this and avoid compiler warning

# best practice

neever use .Wait() or .Result() use GetAwaiter().GetResult();

fire and forget tasks, should await every task,

## questions

should you always use configureawait(false) some apps with no ui won't have a syncronisation context. If ou don't have
onw no need to have one. .NET Core doesn't have sync context so need to call configureaait(false)
