2025-11-17 20:49

Status: [[complete]]

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

## 4. Conditions to work `@Async` properly:
1. Different Class - If `@Async` is applied to the method within the same class from which it is being called then the proxy mechanism is skipped because internal method calls are **NOT INTERCEPTED**
2. Public method: Method annotated with `@Async` must be public, because again AOP interception works only on public method.
## 5. Async and Transaction management: 
1. Transaction context does not transfer from caller thread to new thread, which got created by `@Async`.
2. **Use with precautions**: as new thread will be created and have transaction management too but context is not same as parent thread, So propagation will not work as expected. (Having `@Async` & `@Transactional` on same method not good)
3. Best use-case can be `@Async` method should call `@Transaction` method.


## 6. Return types from @Async:
1. Both Future and Completable Future can be the return types from async method.


## 7. Exception handling: 
1. For async method having some return types we can handle it in get call (future/completable future)
2. For async methods having no return types , need to handle manually by try-catch block inside it.
3. custom **`AsyncExceptionHandler`**: for that, we need to define bean of `AsyncUncaughtExceptionHandler` and implement the method. Then we have to register this bean in configuration of `AsyncConfigurer` which return this bean. (see git repository for example) 
4. If we don't handle it then Spring boots, `SimpleAsyncUncaughtExceptionHandler` will be invoked. 






# References
