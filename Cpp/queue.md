# Queue

## Questions
Why the `pop` function of queue/stack/priority_queue return `void` instead of the element itself?

A: stack(queue)为保证强异常安全性, 如果元素类型没有提供一个保证不抛异常的移动构造函数, 通常会使用拷贝构造函数.
   而pop作用是释放元素, c++98还没有移动构造的概念, 所以如果返回成员, 必须要调用拷贝构造函数, 这时分配空间可能出错,
   导致构造失败, 要抛出异常, 此时top/front的元素可能已经析构, 无法保证容器维持调用pop函数前的状态, 即无法保证强异常安全.

![Queue Memory Layout](https://gitee.com/againxx/image-storage/raw/master/images/queue_layout.png =750x)

