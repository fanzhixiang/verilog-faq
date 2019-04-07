# 如何做好芯片复位(Reset)

> 从0到1不容易，reset也是。


这是一份关于芯片复位(reset)的问题列表。

----

## 1. 复位的作用

- 初始化：比如上电后给计数器一个初始值。
- 出错恢复：比如watchdog可以监测系统出错进行复位。

### 1.1 是否所有包含存储/记忆功能的电路都需要复位？
### 1.2 DFF如果不复位，输出电平是确定值吗？
### 1.3 Latch需要复位吗？
### 1.4 on-chip SRAM没有复位电路，上电后初始值是什么？

----

## 2. 同步/异步复位

- 依赖时钟才能复位的是同步复位
- 不依赖时钟的是异步复位

verilog写法如下:

```verilog
always @(posedge clk) begin
    if(~rst_n) 
        Q <= 1'b0;
    else 
        Q <= D;
end

always @(posedge clk or negedge rst_n) begin
    if(~rst_n) 
        Q <= 1'b0;
    else 
        Q <= D;
end

```

### 2.1 异步复位和同步复位的1个DFF哪个面积大？

### 2.2 异步复位和同步复位各有什么优缺点？

### 2.3 “异步复位，同步释放” （reset synchronizer）

```verilog
reg rst_n_sync_ff0;
reg rst_n_sync_ff1;
always @(posedge clk or negedge rst_n) begin
    if(~rst_n)  begin
        rst_n_sync_ff0 <= 1'b0;
        rst_n_sync_ff1 <= 1'b0;
    end else begin
        rst_n_sync_ff0 <= 1'b1;
        rst_n_sync_ff1 <= rst_n_sync_ff0 ;
    end
end

```

----

## 3. 复位信号从哪里来

- 外部复位
- 电源复位
- watchdog复位
- software复位
- JTAG调试复位

### 3.1 外部复位信号如何去除glitch？

### 3.2 复位的PAD类型如何选择？

### 3.3 上电复位(POR)的时间要多久？

### 3.4 需要几路POR？

### 3.5 低压/掉电复位监测需要多少档位？

### 3.6 watchdog的时钟用哪一个？什么时候开启?

### 3.7 需要多少个软件复位控制接口?

### 3.8 JTAG复位如何跨时钟域？
### 3.9 什么场合没有外部复位？


----

## 4. 复位网络

### 4.1 复位信号有优先级吗？

### 4.2 是电平有效还是脉冲有效？低有效还是高有效？

### 4.3 不同复位信号的控制的模块如何划分？

### 4.4 复位需要保持有效多长时间才能确保整个系统完成复位?（尤其是有多个时钟域的情况下）

### 4.5 clock gating控制信号与复位信号之间的关系？

### 4.6 多级reset-sync-cell级联要注意哪些问题？


----

## 5. 复位响应

复位信号有效后，要考虑系统的行为。

### 5.1 电源和时钟是否稳定了？ 什么情况下可以立即复位？

### 5.2 cpu要做什么处理？

### 5.3 memory的数据怎么办？

### 5.4 如果在系统启动、程序下载、或者中断处理等特殊时刻发生复位如何处理？

### 5.5 通信接口复位之后会处于什么状态？

### 5.6 人机交互接口复位要考虑哪些问题？比如显示接口，声音接口，传感器接口。

### 5.7 SOC中复位释放的先后顺序？

----

## 6. DFT处理

### 6.1 SCAN/BSD/MBIST/Lab test mode需要单独的复位信号吗？

### 6.2 增加DFT bypass模式的reset-sync-cell？

### 6.3 reset-sync-cell的DFF要做扫描吗？对测试覆盖率有什么影响？

### 6.4 双向IO做复位输入，边界扫描如何处理？


----

## 7. 综合与后端

### 7.1 输入复位信号的时序约束:set false path 还是set_input_delay 0 -clock xx？

### 7.2 综合需要设置复位 ideal network，dont_touch_network吗？

### 7.3 后端要给reset做tree吗(CTS)？如何分析异步 RESET 信号树的 SKEW？如何平衡skew和fanout？

### 7.4 什么样的reset信号可以set_false_path？
    
### 7.5 如何进行复位信号的时序和噪声分析?

### 7.6 reset sync cell的时序如何分析?

----

## 8. 测试

### 8.1 lab test(bring up)需要哪些特殊的调试复位信号？

### 8.2 ATE不同测试项之间需要什么样的复位？如何节省测试时间成本？

### 8.3 如何测试系统复位的有效性和可靠性？

### 8.4 电源相关的复位如何测试?

----

## 9. FPGA

### 9.1 怎样使用GSR全局信号作为我的module的reset信号？

### 9.2 做产品的FPGA代码不建议复位

### 9.3 做SOC/ASIC验证如何一直代码到FPGA？

----

## 10. 模拟IP

### 10.1 模拟IP需要复位电路吗？

### 10.2 数模混合仿真的复位过程？


----

## 11. 验证

### 11.1 reset功能如何实现随机化测试？

### 11.2 如何进行寄存器复位初值测试?

### 11.3 如何利用静态分析工具找出复位的设计问题？

### 11.4 后仿中的x状态哪些与复位有关?应该如何处理? reset sync cell的时序违背可以忽略吗？

----

## 12. 软件复位

### 12.1 软件复位之后要等多久？

### 12.2 复位过程中程序内存的状态？

----

## 13. 低功耗

### 13.1 如何实现不同电源域的复位处理?

### 13.2 复位模式下功耗有多少? 复位释放之后是否会由于多个电路同时启动发生瞬间的大电流?

### 13.3 唤醒之后是否需要复位操作?

----

## 14. 常见复位设计错误

### 14.1 没有正确使用reset sync

### 14.2 复位时间不足（复位不完全）

### 14.3 复位与电源、时钟和其他复位信号之间的相互依赖形成死锁

### 14.4 同一信号既用作同步复位，也用作异步复位

### 14.5 复位信号控制的模块过多或过少

### 14.6 复位信号电源域出错

----

## 15. 可靠性设计

### 15.1 如何设计可靠的复位系统？要考虑哪些干扰因素，有哪些措施？

### 15.2 如何设计一个不需要复位的稳定系统？是否可行？

----

## 【参考资料】 关于Reset设计的资料

[1 Clifford E. Cummings, Asynchronous & Synchronous Reset Design Techniques - Part Deux](http://www.sunburst-design.com/papers/CummingsSNUG2003Boston_Resets.pdf)

[2 Reset Testing Made Simple with UVM Phases](http://www.sunburst-design.com/papers/HunterSNUGSV_UVM_Resets_paper.pdf)

[3 Reset verificaiton in soc design](https://s3.amazonaws.com/verificationhorizons.verificationacademy.com/volume-13_issue-3/articles/stream/reset-verification-in-soc-designs_vh-v13i3.pdf)

[4 网上文章，建议FPGA减少不必要的复位逻辑](http://xilinx.eetrend.com/blog/1425)

[5 spyglass CDC入门笔记，来自搜索引擎](https://blog.csdn.net/u011729865/article/details/52918697)

[6 检查上电复位的自动化断言方案，来自路科验证](http://www.eetop.cn/blog/html/28/1561828-433746.html)
