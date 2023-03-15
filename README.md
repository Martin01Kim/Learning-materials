# Learning-materials
模电数电单片机个人总结
## AT89S51

- 8位微处理器：包括运算器与控制器，有位处理器
- 数据存储器（128B RAM）：最多可扩至64KB，片内RAM为高速RAM
- 程序存储器（4KB FLASH ROM）:最多可扩展至64KB
- 4个8位IO口
- 全双工异步串口：4种工作方式
- 2个16位定时器/计数器：有4种工作方式
- 1个看门狗定时器：计数器，检测系统是否跑飞或者死循环，对系统发出复位信号，使系统复位
- 中断系统：5个中断源，5个中断向量（中断服务程序的入口）,2级中断优先级
- 特殊功能寄存器SFR 26个：控制寄存器和状态寄存器，映射在片内RAM区80H~FFH之内
- 低功耗的空闲模式和掉电模式
- 3个程序加密位

相比于89C51，89S51最显著的优点是有一个ISP（在线可编程功能）

![image-20230315103444131](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230315103444131.png)

40个引脚各个功能：

- 电源引脚：Vcc（5V电源），Vss（数字地）
- 时钟引脚：XTAL1（输入源，使用片内震荡源时外接石英晶体，电容，使用外部震荡源时，该引脚悬空），XTAL2（片内震荡源反相放大器输出源）

| 控制引脚 | 功能                                                         |
| -------- | ------------------------------------------------------------ |
| RST      | 复位信号输入，复位时必须加两个机器周期的高电平，正常时应该为TTL低电平 |
| EA*      | EA=1时，决定程序访问的ROM，PC值小于0FFFH时访问片内的FLASH，大于0FFFH时访问片外FLASH；EA=0时，只访问片外FLASH，地址为0000H~FFFFH，一般默认接高电平 |
| ALE      | 访问外部存储器提供的低八位地址锁存信号，将低8位地址锁存在片外地址锁存器中，运行时一直有时钟信号输出，位晶振频率的六分之一，可通过特殊功能寄存器禁止时钟信号输出 |
| PROG*    | 对片内FLASH编程脉冲输入                                      |
| PSEN*    | 片外存储器读选通信号，低有效                                 |

| IO口 |                                                              |                                 |
| ---- | ------------------------------------------------------------ | ------------------------------- |
| P0   | **漏极开路（OD）的双向口**，可作为系统总线的低8位地址线与数据总线的分时复用口，也可作通用IO口，需要加上拉电阻，此时变为准双向口（没有高阻态），可负载8个低功耗型的TTL负载 | 作为总线口输入输出时一定要先写1 |
| P1   | 准双向口，内部含有上拉电阻，可驱动4个低功耗型TTL负载，其中P1.5/P1.6/P1.7是用于对FLASH存储器进行编程和校验的SPI总线，分别是MOSI(串行数据输入)，MISO(串行数据输出)，SCK（移位脉冲引脚） |                                 |
| P2   | 准双向口，内部有上拉电阻，可以作为系统总线的高8位地址总线使用 |                                 |
| P3   | 准双向口，内部有上拉电阻                                     |                                 |

**准双向口使用时要先写1**

**CPU**

- 运算器：对操作数进行算术，逻辑和位操作运算

组成：算术逻辑运算单元ALU，累加器A，位处理器，程序状态字寄存器PSW，以及两个暂存器

**ALU：可以对8位变量进行逻辑运算，算术运算**

**A：使用最频繁的寄存器，可作为ALU的输入数据源之一，也可当作运算结果的存放单元，大多数数据都通过A，数据中转站，为避免瓶颈阻塞，单片机提供了不经过累加器的指令**

**PSW：字节地址为DOH**

![image-20230315111238235](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230315111238235.png)

1. **Cy：进位标志位，当有进位产生时为1，在位处理器时为，是累加器**
2. **Ac：辅助进位标志位，使用BCD码时，当低4位向高4位有进位时为1**
3. **F0：由用户使用的状态标志位，用指令使他置1或清0，控制程序流向**
4. **RS1，RS0：寄存器区选择位，分别用来选择4组不同的寄存器地址，（00H~1FH）**
5. **OV：溢出标志位**
6. **P：奇偶校验位，1表示累加器A中“1”的个数为奇数**

- 控制器

1. PC：程序计数器，是一个独立的16位计数器，用户不可访问，复位时PC位0000H，从程序存储器0000H开始读指令，取一个后自动加1，位宽决定能够访问的程序范围

**存储器：哈佛结构，有各自的访问指令，分为4类**

- 程序存储器(分为片内和片外两部分)：Flash Rom 最多为4KB，片外可扩至64KB

**片内4KB FLASH，地址为0000H~0FFFH，16位地址总线，片外扩至64KB时，地址为0000H~FFFFH，有5个固定单元为中断源入口地址，分别为00003H~0023H，每个依次相隔8位，分别为外部中断0，定时器0，外部中断1，定时器1，串行口**

![image-20230315112839522](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230315112839522.png)

- 数据存储器（分为片内片外两部分）：片内RAM最多为128B，片外可扩至64KB

**程序存储器可扩展最大RAM由地址线决定，89S51地址线为16根，所以可扩展2的16次幂，即64KB，片内片外的低128B地址是相同的，但由于访问指令不同所以不冲突**

![image-20230315115705939](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230315115705939.png)

- 特殊功能寄存器SFR：各功能部件的控制寄存器和状态寄存器

**映射在片内80H~FFH，仅有字节地址末尾为8和0的特殊功能寄存器可以进行位寻址**

![image-20230315115922552](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230315115922552.png)

![image-20230315122332406](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230315122332406.png)

**堆栈指针SP：主要保护断点（保护跳转前程序指针）和现场保护（保护寄存器中的值），复位后默认为07H，使用时需要重新设置堆栈指针地址，一般设在片内RAM最上层**

**寄存器B：主要用于乘除法的数据存储，A*B时，高8位放入B寄存器，低8位放入A寄存器，除法时，商放入A寄存器，余数放入B寄存器**

**辅助寄存器AUXR：DISALE(ALE的禁止允许位，为0时允许)，DISRT0（控制看门狗是否在溢出情况下对系统进行复位，为0时允许复位），WDIDLE（单片机在空闲模式下看门狗是否计数，为0时允许计数）**

**数据指针DPTR0与DPTR1：DPTR0为89C51原有的数据指针，DPTR1为新增加的数据指针，AUXR1寄存器用于选择使用哪个数据指针，为0时使用DPTR0，数据指针也可以作为一个独立的16位寄存器使用，或两个8位的寄存器使用**

**辅助寄存器AUXR1：DPS用于选择使用哪个数据指针，地址为A2H**

**看门狗计数器WDT：14位计数器和看门狗定时器复位寄存器**

- 位地址空间：211个可寻址位，128片内RAM，83位SFR区

128位在RAM中20H~2FH单元中，每个单元为8位，一共128位，每一位可以置1清0，也可以进行8位的读或写

剩余的位在特殊功能寄存器中，一共有11个寄存器可供位寻址，一共88位，由5位未用

![image-20230315104510770](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230315104510770.png)



**串行IO口属于带锁存功能的特殊寄存器，字节地址分别为80H,90H,A0H,B0H**

### 时钟电路与时序

时钟电路产生必须的控制信号，严格按时执行指令，执行程序时，CPU首先取指令，然后译码，由时序电路产生的一系列控制信号完成规定的操作

时序信号分为两类

- 对片内各个功能部件进行控制，用户无需了解
- **对片外存储器或I/O的控制**

**时钟频率直接影响单片机运行速度**

分为两种

- 内部时钟方式：内部集成了一个高增益的反相放大器，外部只需要接一个晶振（11.0592）两个电容即可
- 外部时钟方式：利用现成的外部振荡器产生脉冲信号，一般用于控制多个单片机，使用外部振荡器时XLAT2要悬空

时钟周期：时钟信号的基本时间单位

机器周期：单片机完成一个基本操作所需要的时间，一个机器周期可能包含若干个时钟周期，S51位12个时钟周期为一个机器周期，**一个机器周期有6个状态，1个状态有2拍，一拍代表一个时钟周期**

指令周期：执行一条指令所需要的时间，一般一个指令周期为一个机器周期

**复位时只需要在RST引脚给一个两个机器周期的高电平即可复位**

**单片机最小系统：单片机，时钟电路，复位电路**

### 低功耗模式

**空闲模式IDLE：切断驱动CPU的时钟，退出方式：响应中断，硬件复位**

**掉电保持模式PD：切断所有时钟，维持单片机中RAM，特殊功能寄存器中的内容，该模式可以由内部电源供电**

PCON特殊功能寄存器（87H）：

- SMOD：串行通信波特率的选择
- GF1：通用标志位
- GF0：通用标志位
- PD：掉电保持模式控制位，为1时进入掉电保持模式
- IDL：空闲状态控制位，为1时进入空闲状态

## 总线协议

并行：同一时间总线能发若干个位数的数据

串行：同一时间总线只发一位的数据，并一直维持这种传送方式

单工：A只能给B传送数据

双工：A可以给B传送数据，也可以从B接受数据

半双工：接收数据，传送数据不能同时进行

全双工：接收，传输可以同时进行

**波特率：串口通信速度(BPS)，每秒钟能传送位数的个数**

### 指令系统

寻址方式：指令中说明操作数所在位置的方法

- 寄存器寻址：如MOV A，Rx 将Rx中的数送入A累加器中，Rx为当前使用的寄存器组中的R0~R7，即RAM中的00H~1FH
- 直接寻址：如MOV  A，40H表示把RAM中40H所指向的数据送入累加器A中，也可以MOV   30H , 40H意思为把40H所指向的数据送入30H中，**是访问片内所有特殊功能寄存器的唯一方式**
- **寄存器间接寻址：如MOV A , @Ri (I=0或1)     表示Ri中存放的是操作数的地址，通过该地址找到该数据存到累加器A中**
- 立即数寻址方式：如 MOVC A ,#40H ，表示直接将40H送给累加器A
- **基址加变址寻址方式：基址寄存器只能是PC或DPTR，变址为累加器A，如MOV A , @A+DPTR，两者相加作为16位地址进行寻址**
