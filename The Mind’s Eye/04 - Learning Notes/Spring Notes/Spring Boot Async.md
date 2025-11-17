2025-11-17 20:49

Status: [[ongoing]]

Tags: [[Spring Boot]]


# Spring Boot Async

## 1. ThreadPool: 
- It is collection of threads, which are available to perform the submitted task.
- Once task is complete the thread goes back to pool and wait for new task, i.e. It can be reused.
- In java thread pool created by `ThreadPoolExecutor`.

## 2. Async annotation:
- It is used to mark the method that should run asynchronously.
- Runs in new thread, without block main thread.
- Also need to enable by using `EnableAsync`.

## 3. How does @Async creates new thread? 
1. first it looks for default executor, if not found then initialise `SimpleAsyncTaskExecutor`
2. During application startup, spring boot looks for `ThreadPoolTaskExecutor` bean
3. We can create our own threadPoolTask executor bean. (better because of default has too much of size)
4. Overall its always better to define our own executor bean.







# References
