
# 【每日一题】一起学veirlog

第一季 20180714 - 20181020

## 重要声明
**读书和实践是学习Verilog的正确途径**。
本产品**不能**代替verilog的正规学习，同时可能有上网成瘾、观点误导等副作用，请谨慎使用。

## 001. 
画出CMOS反相器的电路原理图。

## 002. 
反向器的速度与哪些因素有关？什么是转换时间（transition time）和传播延迟（propagation delay）？

## 003. 
解释一下Vih，Vil，Vol，Voh，Vt。

## 004. 
什么是原码，反码，补码，符号-数值码。以4bit为例，给出各自表示的数值范围。

## 005. 
十进制转换为二进制编码： 
127， 
（-127）， 
127.375， 
（-127.375）

## 006. 
画出CMOS三态缓冲器的电路原理图，解释一下高阻态。

## 007. 
什么是open-drain output？

## 008. 
只用2输入mux，实现与，或，非，异或。2输入mux定义为
```verilog
o = s ? a : b;
```

## 009. 
相同面积的cmos与非门和或非门哪个更快？

## 010. 
说明代码中w1和 w2对应电路的具体区别: 
```verilog
wire [2:0] val; 
wire w1 = val > 0; 
wire w2 = val >= 0;
```
## 011. 
什么是竞争和冒险？

## 012. 
设计1bit全加器，采用verilog描述并画出门级电路图。

## 013. 
设计2-4译码器。采用verilog描述并画出门级电路图。

## 014. 
设计BCD译码器，输入0~9。采用verilog描述并画出门级电路图。

## 015. 
用verilog设计8bit奇偶校验电路。

## 016. 
用verilog描述一个多路复用器，输入的通道数目N，每一路的位宽为M。

## 017. 
用verilog实现 `z = abs(x - y) `
1) x和y是8bit无符号数 
2) x和y是8bit有符号数（2补码）

## 018. 
用verilog实现取整函数（ceil、floor、round）。以5bit为例，小数部分1位，取整后保留4bit。 

```verilog
wire [4:0] data; 
wire [3:0] data_ceil;
wire [3:0] data_floor; 
wire [3:0] data_round;
```

## 019. 
用verilog实现乘法`y = a * b` 
a和b都是8bit，考虑三种情况： 
1) 都是无符号数 
2) 都是有符号数 
3) a是有符号数，b是无符号数

## 020. 
输入一个8bit数，统计其中1的个数。

## 021. 
求三个数的最大值：
`y = max(a,b,c)`

```verilog
 wire [3:0] a,b,c;
```

## 022. 
画一个D触发器的电路图。

## 023. 
说明D触发器与Latch的区别。

## 024. 
解释一下D触发器的建立时间与保持时间。

## 025. 
解释一下Latch的建立时间与保持时间。

## 026. 
用verilog实现1bit信号边沿检测功能，输出一个周期宽度的脉冲信号。 
1) 上升沿 
2) 下降沿 
3) 上升沿或者下降沿

```verilog
input clk, rst_n, data; 
output data_edge; 
```

## 027. 
用verilog实现一个4bit二进制计数器。 
1) 异步复位 
2) 同步复位

```verilog
input clk, rst_n; 
output [3:0] o_cnt;
```

## 028. 
用verilog实现串并转换。
1) lsb优先 
2) msb优先

```verilog
input clk, rst_n, data_i; 
output [7:0] data_o; 
```
## 029. 
序列检测器：有“101”序列输入时输出为1，其他输入情况下，输出为0。画出状态转移图，并用verilog描述。 
```verilog
input clk, rst_n, data; 
output flag_101;
```

## 030. 
用verilog实现两路数据的乘法运算，要求只使用1个乘法器。 
```verilog
input clk, rst_n; 
input sel_x; 
input [7:0] da_x_y; 
input [7:0] db_x_y; 
output reg [15:0] dout_x_y;
```

## 031. 
名词解释：
- ROM
- RAM
- SRAM
- DRAM
- SDRAM
- EEPROM
- DDR
- FLASH

## 032. 
用verilog实现一个深度16，位宽8bit的ROM，初始值等于对应地址加上`0xA0`。 
```verilog
moudule rom_16x8 ( 
... 
); 
... 
endmodule
```

## 033. 
画出SRAM bit cell结构图。

## 034. 
用verilog实现一个单端口sram，深度16，位宽8bit。支持片选，读写请求，要求代码可综合。 
```verilog
module spram_16x8 ( 
    input clk, 
    input [3:0] addr, 
    input [7:0] din, 
    output [7:0] dout, 
    ... 
); 
... 
endmodule
```

## 035. 
用verilog实现一个同步双端口sram，深度16，位宽8bit。A口读出，B口写入。支持片选，读写请求，要求代码可综合。 
```verilog
module dpram_16x8 (
    input clk, 
    input [3:0] addr_a, 
    output [7:0] dout_a, 
    input [7:0] din_b, 
    input [3:0] addr_b, 
    ... 
); 
... 
endmodule
```

## 036. 
用verilog实现一个异步双端口ram，深度16，位宽8bit。A口读出，B口写入。支持片选，读写请求，要求代码可综合。
 
```verilog
module dpram_16x8 ( 
    input clk_a, 
    input [3:0] addr_a, 
    output [7:0] dout_a, 
    ...
    input clk_b, 
    input [7:0] din_b, 
    input [3:0] addr_b, 
    ... 
); 
... 
endmodule
```
## 037. 
用verilog实现一个同步双端口ram，深度16，位宽8bit。A口可读可写，B口可读可写。支持片选，读写请求，要求代码可综合。 
```verilog
module dpram_16x8 ( 
    input clk, 
    input [7:0] din_a, 
    input [3:0] addr_a, 
    output [7:0] dout_a, 
    ... 
    input [7:0] din_b, 
    output [7:0] dout_b, 
    input [3:0] addr_b, 
    ... 
); 
... 
endmodule
```

## 038. 
用verilog实现一个3-tap低通FIR滤波器，输入输出为8bit无符号数，滤波器系数`[1/4 1/2 1/4]` 
```verilog
module fir_lpf_3tap ( 
    input clk, 
    input rst_n, 
    input [7:0] din, 
    output [7:0] dout 
); 
...
endmodule
```

## 039. 
用verilog实现一个3-tap低通FIR滤波器，输入输出为8bit无符号数，滤波器系数`[1/4 1/2 1/4]`，支持bypass功能：fir_bypass为1时输出原始数据。
 
```verilog
module fir_lpf_3tap ( 
    input clk, 
    input rst_n, 
    input fir_bypass, 
    input [7:0] din, 
    output [7:0] dout 
); 
...
endmodule
```

## 040. 
用verilog实现一个低通FIR滤波器，输入输出为8bit无符号数，滤波器系数根据mode选择： 
mode 0：bypass 
mode 1：[1 2 1]/4 
mode 2：[1 2 2 2 1]/8 
mode 3：[1 2 3 4 3 2 1]/16 

```verilog
module fir_lpf ( 
    input clk, 
    input rst_n, 
    input [1:0] mode, 
    input [7:0] din, 
    output [7:0] dout 
); 
...
endmodule
```

## 041. 
用verilog实现一个参数化的FIR滤波器。可配置参数包括 1. 输入输出数据位宽N 2. 滤波器阶数T 3. 滤波器系数位宽M （输入数据与滤波器系数为无符号数）

## 042. 
用verilog实现一个3-tap低通FIR滤波器，Y通路输入输出为8bit无符号数，滤波器系数[1/4 1/2 1/4]。C通路bypass输出。 
```verilog
module fir_lpf_3tap_YC ( 
    input clk, 
    input rst_n, 
    input [7:0] yin, 
    output [7:0] yout, 
    input [7:0] cin, 
    output [7:0] cout 
); 
...
endmodule
```
## 043. 
用verilog实现 `y(n) = x(n) + x(n-1) + x(n-2) + x(n-3) + x(n-4)+ x(n-5)+ x(n-6)+ x(n-7)` 输入x是8bit无符号数。

## 044. 
用verilog实现 `y(n) = 0.75*x(n) + 0.25*y(n-1)` x, y是8bit无符号数。

## 045. 
用verilog实现二分频。

## 046. 
用verilog实现三分频电路，要求输出50%占空比。

## 047. 
画出clock gating cell的原理图。

## 048. 
用verilog实现静态时钟切换电路。外部管脚输入sel，clk，testclk。sel为1输出clk，sel为0输出testclk。 
```verilog
module clkmux_DONTCH ( 
    input sel, 
    input clk, 
    input testclk, 
    output clko 
); 
... 
endmodule
```

## 049. 
用verilog实现glitch free时钟切换电路。输入sel，clka，clkb，sel为1输出clka，sel为0输出clkb。

## 050. 
解释一下亚稳态。

## 051. 
用verilog实现异步复位同步释放电路。

## 052. 
用verilog实现异步复位同步释放电路，支持测试模式的复位信号切换。

## 053. 
用verilog实现4bit约翰逊(Johnson)计数器。

## 054. 
用verilog实现4bit环形计数器：复位有效时输出0001，复位释放后依次输出0010，0100，1000，0001，0010...

## 055. 
用verilog实现按键抖动消除电路，抖动小于15ms，输入时钟12MHz。

## 056. 
用verilog实现PWM控制呼吸灯。呼吸周期2秒：1秒逐渐变亮，1秒逐渐变暗。系统时钟24MHz，pwm周期1ms，精度1us。

## 057. 
在clk a时钟域的一个单周期脉冲信号，如何正确的传递到clk b时钟域? 要考虑clk a和b的各种不同频率/相位的场景。

## 058. 
用verilog实现一个同步FIFO，深度16，数据位宽8bit。

## 059. 
用verilog实现一个异步FIFO，深度16，数据位宽8bit。

## 060. 
用verilog实现一个异步FIFO，深度17，数据位宽8bit。

## 061. 
FIFO深度计算： 写入时钟20MHz，读出时钟40MHz，每1000个时钟周期写入500个数据，每4个时钟周期读出1个数据，读写数据位宽一致。

## 062. 
用verilog实现valid-ready握手协议。 
```verilog
module handshake_pipe ( 
    input clk, 
    input rst_n, 
    input valid_i, 
    output ready_o, 
    input din, 
    output valid_o, 
    input ready_i, 
    output dout 
); 
... 
endmodule
```

## 063. 
用verilog实现支持valid-ready握手协议的下采样电路：每输入2个数据，输出1个数据。 
```verilog
module handshake_pipe_ds ( 
    input clk, 
    input rst_n, 
    input valid_i, 
    output ready_o, 
    input din, 
    output valid_o, 
    input ready_i, 
    output dout 
); 
... 
endmodule
```

## 064. 
用verilog实现支持valid-ready握手协议的上采样电路：每输入1个数据，输出2个数据。约定clk频率高于输出数据速率。 
```
module handshake_pipe_us ( 
    input clk, 
    input rst_n, 
    input valid_i, 
    output ready_o, 
    input [7:0] din, 
    output valid_o, 
    input ready_i, 
    output [7:0] dout 
); 
    ... 
endmodule

```

## 065. 
用verilog实现支持valid-ready握手协议的分路电路：输入1路数据，输出2路数据。 
```verilog
module handshake_pipe_split ( 
    input clk, 
    input rst_n, 
    input valid_i, 
    output ready_o, 
    input [7:0] din, 
    output valid_1_o, 
    input ready_1_i, 
    output [7:0] dout_1, 
    output valid_0_o, 
    input ready_0_i, 
    output [7:0] dout_0 
); 
... 
endmodule
```

## 066. 
用verilog实现支持valid-ready握手协议的合并电路：输入2路数据，输出1路数据。 
```verilog
module handshake_pipe_merge ( 
    input clk, 
    input rst_n, 
    input valid_0_i, 
    output ready_0_o, 
    input [7:0] din_0, 
    input valid_1_i, 
    output ready_1_o, 
    input [7:0] din_1, 
    output valid_o, 
    input ready_i, 
    output [15:0] dout 
); 
... 
endmodule
```

## 067. 
解释一下valid-ready握手传输中的bubble问题，如何解决？

## 068. 
使用valid-ready多级流水时，ready信号通路上组合逻辑过长会带来什么问题？怎样解决？

## 069. 
用verilog实现配置寄存器接口。 
地址0 ：可读可写RW
地址1 ：只读RO 
地址2 ：只写，自动清0
地址3 ：保留 

```verilog
module blk_ctrl ( 
    input clk, 
    input rst_n, 
    input wr, 
    input [1:0] addr, 
    input [7:0] wdata, 
    input rd, 
    output [7:0] rdata 
); 
... 
endmodule
```
## 070. 
解释一下触发器的setup和hold，在芯片使用中如果遇到时序问题，怎样区分是setup还是hold的问题？

## 071. 
解释一下`multi cycle path`

## 072. 
用verilog实现16bit复数乘法器。

## 073. 
把十进制数`8.15`转换为单精度浮点数。

## 074. 
把十进制数`-6.125`转换为双精度浮点数。

## 075. 
用verilog实现32位浮点数加法。

## 076. 
用verilog实现16位浮点乘法。

## 077. 
解释`booth`乘法器实现原理。（以radix 4为例）

## 078. 
用verilog实现4位超前进位加法器。

## 079. 
用verilog实现8位桶形移位寄存器。

## 080. 
用verilog实现一个深度为16的CAM。

## 081. 
用verilog实现8位无符号除法。

## 082. 
用verilog实现8位定点数开平方。

## 083. 
用verilog实现`log2(x)`，输入x为16bit无符号数。

## 084. 
设计1MHz正弦波发生器。

## 085. 
用verilog实现三输入round robin仲裁器。

## 086. 
用verilog实现图像行缓冲（line buffer），输入数据Yi为8bit，每行数据1920个，要求同时输出3行，即当前数据Y0，延迟1行对应的数据Y1，延迟2行对应的数据Y2。

## 087. 
用verilog实现图像的二维滤波器。输入输出图像分辨率1920x1080，8bit，YUV422。滤波器为3*3，系数8bit有符号数。滤波操作只针对Y进行处理，UV直通。

## 088. 
用verilog实现MAC单元：输入32路数据A，32路数据B，都是8bit有符号数。输出32路A乘以B的累加和。

## 089. 
用verilog实现激活函数`ReLU`，输入为16bit有符号数。

## 090. 
用verilog实现激活函数sigmoid：`f(x) = 1/(1+e^-x)`，输入x为16bit有符号数。

## 091. 
用verilog实现max pooling函数，kernel 7x7，数据16bit有符号数。

## 092. 
用verilog实现排序算法。输入数据为128个16bit有符号数。

## 093. 
用verilog实现一个APB接口的单口RAM，深度1024，位宽32bit。

## 094. 
用verilog实现一个AHB接口的单口RAM，深度1024，位宽32bit。

## 095. 
用verilog实现一个AXI接口的单口RAM，深度1024，位宽32bit。

## 096. 
解释一下DMA控制器的基本功能与实现。

## 097. 
使用verilog开发项目需要用到哪些工具？

## 098. 
使用verilog实现APB接口的I2C模块，兼容标准协议。

## 099. 
举例说明3条使用verilog开发项目的经验或教训。
