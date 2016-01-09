# 核心组件：InactivityCop 状态机

InactivityCop是对早期的超时机制的改进，这个改进降低了EventSystem的压力。

原来的超时控制完全依靠EventSystem的定时事件来实现，导致EventSystem的事件队列内容纳了大量的事件。

对于一个 NetVConnection 的两种超时类型，10K连接就有20K事件长期塞在EventSystem的内部队列里。

因此ATS或者是更早的Inktomi公司，重构了超时管理，提出了InactivityCop状态机，专门用来支持 NetVConnection 的两种超时。

![How the InactivityCop works](https://cdn.rawgit.com/oknet/atsinternals/master/CH02-IOCoreNET/CH02-IOCoreNet-002.svg)