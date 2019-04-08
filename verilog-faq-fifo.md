# 关于FIFO的一些问题 

## 吐槽

- 曾经我以为我会写FIFO......然后发现就它出的bug多
- 数字设计每个面试几乎必问
- 深度啦，满了怎么办啦，有那么多讲究吗？我很好奇
- FIFO是比较经典的电路，里面涉及了不少常用的基础知识和概念，所以大家都喜欢问
- 初学者都是基于cummings那片文章的异步FIFO
- 所以网上有很多FIFO的刷题库
- 我觉得异步FIFO没什么难的啊，考虑全面点就行了。
- 真的吗？


## 三个哲学基本问题

- why ：FIFO是集成模块，会写吗？会用吗？
- How ：基于经典面试问题，结合开源模块讨论。
- What：能写会用，找到开源可用的东西，不再为了FIFO而困惑。


## 什么是FIFO

- First-In-First-Out，先入先出队列，不支持随机访问。


## 哪些功能模块/场景中会用到FIFO？

- 低速外设，比如UART
- DMA
- command/data fifo
- 跨时钟域接口

## 同步FIFO和异步FIFO？

- 读写共用一个时钟的是同步FIFO
- 同频不同相位？
- 同源时钟（比如读时钟是写时钟的2分频）？


## FIFO的存储是用dff还是memory block？

- dff
- 伪双口memory
- 真双口memory


## 针对低功耗应用的FIFO设计有哪些策略？

- clock gating (读、写、memory)
- power gating

## 异步FIFO的设计要注意哪些问题？

- 空满信号的产生: 参考cummings文章
- 格雷码跨时钟域
- [关于异步fifo的快转慢的问题](https://zhuanlan.zhihu.com/p/22681019)

## 异步FIFO在验证、综合、DFT和后端流程有哪些注意事项？

- false path？ 通过max delay, min delay
- timing check？
- scan/mbist?

## FIFO深度计算？

参考文章[异步FIFO最小深度计算方法及原理分析](https://blog.csdn.net/u011412586/article/details/10241585/)

## 异步FIFO读写时钟频率相差很大(比如100倍)，会遇到什么问题？

- 慢时钟采快时钟，会出现假的空、满现象。

## 深度不是2^N的异步FIFO如何设计？

- 格雷码设计

来自[eetop论坛的讨论](http://bbs.eetop.cn/viewthread.php?tid=439464&extra=&page=1)
> 非2^N的也可以。只有是偶数深度都可以。用的时候把2^N的gray code头尾去掉相同个数个值就可以啦。
> 
> 我们用6来举例：
> 0-7的gray code如下：
> 0 --> 000
> 1 --> 001
> 2 --> 011
> 3 --> 010
> 4 --> 110
> 5 --> 111
> 6 --> 101
> 7 --> 100 
> 
> 那么0-5的就是
> 1(0) --> 001
> 2(1) --> 011
> 3(2) --> 010
> 4(3) --> 110
> 5(4) --> 111
> 6(5) --> 101

[How to generate Gray Codes for non-power-of-2 sequences](https://www.eetimes.com/document.asp?doc_id=1274581&page_number=1)



## 你用过哪些FIFO的IP？

- designware IP


## FPGA FIFO 使用

- Intel/Altera
- Xilinx
- Lattice 


## 开源的FIFO IP资源

- [NVDLA代码中的异步FIFO](https://github.com/nvdla/hw/blob/nvdlav1/vmod/nvdla/csb_master/NV_NVDLA_CSB_MASTER_falcon2csb_fifo.v)


## 资料推荐

- http://www.sunburst-design.com/papers/CummingsSNUG2002SJ_FIFO1.pdf
- http://www.sunburst-design.com/papers/CummingsSNUG2002SJ_FIFO2.pdf
- [Vijay A.Nebhrajani 的《异步FIFO结构》英文原版](http://bbs.eetop.cn/thread-460997-1-1.html)
- [华为内部FIFO经验](http://bbs.eetop.cn/thread-286177-1-1.html)

