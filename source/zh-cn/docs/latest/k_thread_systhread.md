title: 系统线程 - System Threads
---

*系统线程（system thread）* 是指在系统初始化期间由内核自动创建的线程。

# 概念

内核在系统启动时自动创建主线程和空转线程。

- **主(main)线程**

 </br>该线程会先执行内核的初始化，然后调用应用程序的 `main()` 函数（如果存在）。

 </br>默认情况下，主线程的优先级是 0，即优先级最高的可抢占式线程。如果所配置的内核不支持抢占式线程，则其优先级是 -1，即优先级最低的协作式线程。

 </br>主线程是执行内核初始化时，或者执行应用程序的 `main()` 函数时的必须线程。这意味着，如果该线程被异常终止，内核会认为产生了一个致命错误。如果应用程序没有定义 `main()` 函数，或者如果它执行后正常返回了，主线程就结束了，此时不会抛出错误。

 </br>

- **空转(idle)线程**

 </br>当系统没有其它工作需要执行时，会执行该线程。如果可能，空转线程应当激活板子的电源管理功能，以达到省电的目的；否则，该线程简单地执行一个“do nothing”的循环。空转线程永远不会结束。只要系统一直在运行，它就一直存在。

 </br>空转线程的优先级是系统所配置的最低优先级。如果它是协作式线程，它会不断地释放 CPU，以使应用程序线程需要运行时能顺利运行。

 </br>空转线程也是必须线程，因此如果它被异常终止了也会导致致命的系统错误。

 </br>

内核也可能会创建额外的系统线程，这依赖于应用程序指定的开发板配置选项。例如，使能系统工作队列将创建一个系统线程，该线程负责为提交给它的工作提供服务。（参考 [工作队列]()。）

# 实现

## 写一个 main() 函数

内核执行完初始化操作会就会执行应用程序提供的 `main()` 函数。内核不会向该函数传递任何参数。

下面这几行代码总结了 `main()` 函数的一般写法。在实际应用中，该函数可以被设计得非常复杂。

```c
void main(void)
{
    /* initialize a semaphore */
    ...

    /* register an ISR that gives the semaphore */
    ...

    /* monitor the semaphore forever */
    while (1) {
        /* wait for the semaphore to be given by the ISR */
        ...
        /* do whatever processing is now needed */
        ...
    }
}
```

# 建议的用法

如果应用程序只需要一个线程就能完成，不要再定义额外的线程，直接使用主线程就可以了。

# 配置选项

相关的配置选项：
- `CONFIG_MAIN_THREAD_PRIORITY`
- `CONFIG_MAIN_STACK_SIZE`
- `CONFIG_IDLE_STACK_SIZE`


# API

无。