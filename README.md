# Learning-materials
模电数电单片机个人总结
## 电阻

## 电容

电容器的串并联分压公式

**串联公式：C=C1C2/(C1+C2)**

**并联公式C=C1+C2+C3**

**补充部分：串联分压比V1=C2/(C1+C2)V…电容越大分得电压越小，交流直流条件下均如此**

**并联分流比I1=C1/(C1+C2)I…电容越大通过的电流越大**

电容阻抗与其频率有关，理想情况下频率越高阻抗越小，但实际情况下电容可看作一个电容电感串联的高效电路，因为电感频率越高阻抗越大，所以当频率高于电容谐振频率时，电容实际会表现出电感特性

### 电容降压

利用电容容抗来取代回路中需要的电阻

**优点:减少了降压元件所消耗的功率，既可以降压，又不消耗电能**

**实际使用时要注意:**

要为电容提供一个可供其放电的回路，用电阻与电容串联，以防止实际使用后断电时触摸插孔会使电容放电导致触电。

因负载通常都需要直流，所以回路中一般使用二极管来构成回路，由此衍生出如下两种降压电路

- **半波整流电路**

- 电路中串联，并联两个二极管，D1为正半周期给RL提供负载，D2为C1提供放电回路，此时负载的电流为全波整流的一半，负半周期的电能送回给电源

- **全波整流电路**
- 为组件RL，正半周期都提供了良好的负载，此时负载的电流翻倍

- 实际使用时，因为电路开启时，电容相当于短路，需要电容与一个电阻串联，防止后续器件烧伤，串联电阻的电阻值选取标准以后续器件的最小额定电流为准，当然实际情况电压会比额定电压大，所以电阻计算时应视情况而定

### 电容滤波

由于大电容的制作工艺是多个导线缠绕制成，所以大电容工作时会表现出电感特性，即在高频信号下表现不好，而小电容因其体积小，所以其电感特性不明显，在高频信号下表现良好，所以可以采用大电容并联小电容的接法去过滤电路中的高频噪音和低频噪音

## 电感

**电感的电流不能突变**

### 电感与磁珠的区别

1. 电感是储能元件，磁珠是能量转换器件
2. 电感多用于滤波回路，磁珠多用于信号回路
3. 电感多用于中低频网络，磁珠常用于高频电路中

## 二极管

P型材料：用+3价硼原子从+4价的硅原子抢夺一个电子，硼原子带负电，硅原子留下空穴带正电，空穴即为多子

N型材料：用+5价磷原子，给予+4价硅原子一个电子，磷原子带正电，硅原子多一个电子带负电，电子为多子

PN结原理：扩散运动（多子），漂移运动（少子）

- 施加正偏电压时，扩散运动增强，空间电荷区变窄
- 施加反偏电压时，漂移运动增强，空间电荷区变宽

伏安特性曲线：


**导通电压：由于本身的扩散运动会使PN结内部产生一个内电场，外部施加正向电压时其电场需要大于内电场，才能增强其扩散运动产生电流，硅二极管一般为0.7V**

**反向饱和电流：**

- **施加反向电压时的与横轴平行的电流，当施加反向电压时，几乎所有的少子都参与了漂移运动，所以外部来看反向饱和电流恒定**
- **当大到一定程度时，破坏了PN结结构，价电子挣脱共价键的束缚形成电流，击穿电压**

uT为温度的电压当量

在电路中，对二极管同时施加直流电源和交流电源，则可将二极管视作一个电阻



### 二极管的反向恢复过程

理想情况下，当电路中给予二极管一个远大于导通电压的电压时，突然使其反向，电路中的电流应立即截止，但实际情况为，电路中电流会先反向，而后缓慢截止

称之为二极管的反向恢复过程

产生的原因：

- 在正向导通时，P区的空穴与N区的电子并不会在空间电荷区中立即复合，而是在一定的路程内，边漂移边扩散，使P区积攒电子，N区积攒空穴
- 突然间施加反向电压时，P区的电子，与N区的空穴会被拽回到相应的区域，形成反向漂移电流，所以会导致UI图中的反向电流
- 漂移的过程，电子与空穴复合，电流会慢慢减小，直至变为正常的反向饱和电流

因为二极管的反向恢复过程，所以二极管不能再快速连续的脉冲下当做开关，

### 肖特基二极管

对应于传统二极管，肖特基二极管的优点是

- 反向恢复时间非常短
- 导通电压低
- 漏电流比较大，反向击穿电压比较低

对应于场效应管，肖特基二极管的区别是

- 肖特基二极管低功耗，超高速，反向恢复时间短，一般用于整流电路，场效应管是三极管，输入阻抗高，功耗低，噪音小，漏电流小，开关特性好，一般用于放大电路

### 两个二极管串联的意义

当要求二极管承受的电压值大于其反向击穿电压时，一个二极管无法满足要求，此时就可以用两个二极管串联，利用二极管反向的反向电阻分压，将反向电压平均分配，但由于每个二极管的反向电阻不一定相同，则应每个二极管再并联一个电阻，使其电阻近乎相同，从而做到均分反向电压

### 续流二极管

消除回路中大量的反向电动势，保护元器件

在图3 中KR 在VT 导通时，上面电压为上正下负，电流方向由上向下。在VT 关断时会，KR中电流突然中断，会产生感应电势，其方向是力图保持电流不变，即总想保持KR 电流方向为由下至下。这个感应电势与电源电压迭加后加在ＶＴ两端，容易使ＶＴ出穿。为此加上ＶＤ，将ＫＲ产生的感应电势短路掉，电注是你所说的“顺时针方向在二极管和继电器所的小回路里面流动”，从而保护ＶＴ

### 瞬态电压抑制器

利用二极管的反向击穿原理，与器件并联接入，当电路中电压过大，大于TVS的反向击穿电压时，TVS会从高阻态变为低电阻状态，同时将器件两端电压钳制在较低水平，保护电路，当电压恢复正常后，TVS管又变为高阻态，电路正常工作

## 三极管

### MOS管

- 结型：利用PN结特性，使用时要让栅源电压小于0，栅源电压越小，产生沟道越窄，同样会产生夹断现象，**VGS不能大与0，会使GS的PN结导通**

- 绝缘栅型：栅极下加入一个SIO2绝缘层，利用电场力吸引电子产生沟道，使漏源导通

#### 主要特性

因为MOS管栅极无电流，输入端无伏安特性曲线，所以没有输入特性，故用特殊的转移特性表示其特性曲线

### 三极管与MOS的对比

1）．场效应管的源极S、栅极G、漏极D分别对应于三极管的发射极e、基极b、集电极c，它们的作用相似，图1-6-A所示是N沟道MOS管和NPN型晶体三极管引脚，图1-6-B所示是P沟道MOS管和PNP型晶体三极管引脚对应图。

2)．场效应管是电压控制电流器件，由VGS控制ID，普通的晶体三极管是电流控制电流器件，由IB控制IC。MOS管道放大系数是（跨导gm）当栅极电压改变一伏时能引起漏极电流变化多少安培。晶体三极管是电流放大系数（贝塔β）当基极电流改变一毫安时能引起集电极电流变化多少。

3)．场效应管栅极和其它电极是绝缘的，不产生电流；而三极管工作时基极电流IB决定集电极电流IC。因此场效应管的输入电阻比三极管的输入电阻高的多。

4)．场效应管只有多数载流子参与导电；三极管有多数载流子和少数载流子两种载流子参与导电，因少数载流子浓度受温度、辐射等因素影响较大，所以场效应管比三极管的温度稳定性好。

5)．场效应管在源极未与衬底连在一起时，源极和漏极可以互换使用，且特性变化不大，而三极管的集电极与发射极互换使用时，其特性差异很大，b 值将减小很多。

6)．场效应管的噪声系数很小，在低噪声放大电路的输入级及要求信噪比较高的电路中要选用场效应管。

7)．场效应管和普通晶体三极管均可组成各种放大电路和开关电路，但是场效应管制造工艺简单，并且又具有普通晶体三极管不能比拟的优秀特性，在各种电路及应用中正逐步的取代普通晶体三极管，目前的大规模和超大规模集成电路中，已经广泛的采用场效应管。

### IGBT

由一个三极管与MOS管组合而成，使其有MOS管高输入阻抗的优点，同时还有三极管双载流的优点。实现驱动功率小，饱和压降低的好处

### 作为开关使用时，MOS相比于三极管的好处

- 开关特性好:由于MOS管只靠多子导电，所以不存在少子储电特性，因此关断很迅速
- 输入阻抗高：由于MOS管栅极与衬底中有绝缘层隔开，可以看作为电容，所有有很大的输入阻抗
- 无二次击穿：当三极管温度上升时，会导致集电流电流上升，而集电极电流上升则会导致温度上升，形成恶循环，而mos管则具有与三极管相反的电流，温度特性，当温度上升时，电流反而会变小，从而温度会下降
- MOS管导通后呈现纯阻性：三极管在饱和状态下时，可看作两个正偏的二极管，有极低的压降，但是这个压降为非线性电阻，不能利用欧姆定律去计算，而MOS管导通时呈现纯阻性状态，可以利用欧姆定律计算，从而可以使其并联在电路中，所以一个MOS管功率不够时，则可以多个MOS管并联

## 晶振

通电时产生机械振荡，施加力时会产生电

### 为什么要外加电容

使晶体两端电容近似相当于负载电容，满足谐振条件使其起振

晶体旁的两个电容要接地，为三点式分压电容，接地点就是分压点

### 为什么外加电阻

晶体的内部芯片电路，可以看作是以一个增益很大的放大器，接入电阻相当于引入反馈，使晶体更稳定的工作

### 晶振为什么不能放置在PCB边缘

会产生EMC辐射干扰电路

### 32.768KHZ晶振作用

32768为2的15次方，作为单片机中的时钟信号，将其15等分即能获得频率为1HZ的信号

## 放大电路

共射级放大电路：

为什么输出电阻很大时，输出相当于电流源，输出电阻很小时，输出相当于电压源

原因：**根据戴维南等效定律，从负载RL向电路看，可以等效为一个电压源和一个电阻串联，所以可得到相应的Uo，Io，根据公式可算出，当R0很大时，负载电阻的变化对电流几乎没影响，但对电压影响很大，R0很小时，负载电阻变化对电压几乎没影响，但对电流影响很大**

放大电路中，射级偏置电压Re的作用：

**将输出与输入之间联系起来，Ic的升高引起Ie升高，从而导致Ue升高，再导致Ube分得的电压下降，导致Ib下降，反过来影响Ic，形成反馈**

Rb2的作用是温度B基级电压，让流过Ib2的电流远大于Ib，可以将Rb1，Rb2，在B点电压近似于两电阻分压

### 复合管

由两个三极管构成，让他在高功率电路上近似看成一个三极管组成的电路构成，放大电路大约为两个三极管放大倍数相乘

### 多级放大电路

## 稳压器

### 串联型稳压器

### 三端稳压器

## 运算放大器

### 同相比例

### 返相比例

### 差动放大器

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

- 数据存储器（分为片内片外两部分）：片内RAM最多为128B，片外可扩至64KB

**程序存储器可扩展最大RAM由地址线决定，89S51地址线为16根，所以可扩展2的16次幂，即64KB，片内片外的低128B地址是相同的，但由于访问指令不同所以不冲突**

- 特殊功能寄存器SFR：各功能部件的控制寄存器和状态寄存器

**映射在片内80H~FFH，仅有字节地址末尾为8和0的特殊功能寄存器可以进行位寻址**


**堆栈指针SP：主要保护断点（保护跳转前程序指针）和现场保护（保护寄存器中的值），复位后默认为07H，使用时需要重新设置堆栈指针地址，一般设在片内RAM最上层**

**寄存器B：主要用于乘除法的数据存储，A*B时，高8位放入B寄存器，低8位放入A寄存器，除法时，商放入A寄存器，余数放入B寄存器**

**辅助寄存器AUXR：DISALE(ALE的禁止允许位，为0时允许)，DISRT0（控制看门狗是否在溢出情况下对系统进行复位，为0时允许复位），WDIDLE（单片机在空闲模式下看门狗是否计数，为0时允许计数）**

**数据指针DPTR0与DPTR1：DPTR0为89C51原有的数据指针，DPTR1为新增加的数据指针，AUXR1寄存器用于选择使用哪个数据指针，为0时使用DPTR0，数据指针也可以作为一个独立的16位寄存器使用，或两个8位的寄存器使用**

**辅助寄存器AUXR1：DPS用于选择使用哪个数据指针，地址为A2H**

**看门狗计数器WDT：14位计数器和看门狗定时器复位寄存器**

- 位地址空间：211个可寻址位，128片内RAM，83位SFR区

128位在RAM中20H~2FH单元中，每个单元为8位，一共128位，每一位可以置1清0，也可以进行8位的读或写

剩余的位在特殊功能寄存器中，一共有11个寄存器可供位寻址，一共88位，由5位未用

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
