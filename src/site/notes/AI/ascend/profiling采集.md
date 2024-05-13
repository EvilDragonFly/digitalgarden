---
{"dg-publish":true,"permalink":"/AI/ascend/profiling采集/","noteIcon":"3"}
---


https://www.hiascend.com/document/detail/zh/CANNCommunityEdition/80RC2alpha001/devaids/auxiliarydevtool/atlasprofiling_16_0016.html

比较原始的profiling采集方法，使用cann相关的工具包，对于训练和推理都可以进行相关的性能采集任务

> [!NOTE] 注意
> 该采集方式是通过服务启动用户工作目录当前的sock文件进行通信的，比如是root用户启动推理任务的话，/root/目录会有一个sock文件，我们启动msprof采集任务的话也需要以root用户启动，如果推理任务的是HwHiAiUser启动的话，msprof也需要使用HwHiAiUser启动，防止msprof找不到对应的sock文件

![Pasted image 20240513101806.png](/img/user/AI/ascend/attachments/Pasted%20image%2020240513101806.png)