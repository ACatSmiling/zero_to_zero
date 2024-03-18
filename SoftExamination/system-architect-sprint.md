*date: 2024-03-13*

## 中央处理单元 CPU

<img src="./system-architect-sprint/image-20240313230046456.png" alt="image-20240313230046456" style="zoom: 50%;" />

CPU 的功能：

- 程序控制
- 操作控制
- 时间控制
- 数据处理

CPU 的组成：

- `运算器`（**数据加工、算术运算、逻辑运算**）
  - 算术逻辑单元 ALU
  - 累加器
  - 状态条件寄存器
  - 缓冲寄存器
- `控制器`（**保证指令执行、处理异常事件**）
  - 指令寄存器
  - 程序计数器
  - 地址寄存器
  - 指令译码器
- `寄存器组`（**保存程序的中间结果**）
- `总线`

>在 CPU 中，（ ）不仅要保证指令的正确执行，还要能够处理异常事件。
>
>A. 运算器
>
>B. 控制器
>
>C. 寄存器
>
>D. 内部总线
>
>【答案】B

## 数据表示

### 二进制转十进制

`无符号的二进制整数`：**从右往左依次用二进制位上的位数乘以 2 的 n 次幂的和（n 大于等于 0）**。

`带符号的二进制整数`：除去**最高位的符号位（1 为负数，0 为正数）**，其余与无符号二进制转化为十进制方法相同。

`小数二进制数`：从小数点后第 1 位上的二进制数字乘以 2 的负一次方，加上第 2 位上的二进制数字乘以 2 的负二次方，以此类推**第 n 位上的二进制数字乘以 2 的负 n 次方**。

>将二进制 1100.101 转化为十进制，结果是（ ）。
>
>A. 12.625
>
>B. 12.75
>
>C. 24.625
>
>D. 24.75
>
>【答案】A

### 十进制转二进制

`转化整数`：

1. 将**整数部分除 2，取余**。
2. 当商不为 0 时，将商作为被除数。
3. 继续除 2 取余，直至商为 0。
4. 将**余数按从下到上的顺序记录**。

`转化小数`：

1. 将**小数部分乘 2，取整**。
2. 如果结果仍有小数，就继续乘 2。
3. 直到小数部分为 0，或者已经达到了精度要求。
4. 将**取整的结果按从上到下的顺序记录**。

>将十进制 11.75 转化为二进制，结果是（ ）。
>
>A. 1011.11
>
>B. 1010.11
>
>C. 1010.01
>
>D. 1011.01
>
>【答案】A

### 原码

**最高位是符号位，0 表示正号，1 表示负号，其余的 n-1 位表示数值的绝对值。**

- 数值 0 的原码表示有两种形式：[+0]~原~ = 0 0000000，[-0]~原~ = 1 0000000。

以带符号位的四位二进制数为例：1010，最高位为 1 表示这是一个负数，其它三位 010，即 $0*2^2+1*2^1+0*2^0=2$，所以 1010 表示十进制数 -2。

>若机器字长为 8，则 +127 和 -0.5 分为表示为（ ）。
>
>A. 0 1111111，0 1000101
>
>B. 0 1111111，1 1000000
>
>C. 1 1111111，0 1000000
>
>D. 1 0000000，1 1000101
>
>【答案】B

### 反码

**原码最大的问题就在于一个数加上它的相反数不等于 0。**例如：1~原~ = 0001，-1~原~ = 1001，则 1~原~ + (-1~原~) = 1010，即得出 1 + (-1) = -2，这很明显是错误的。

`正数的反码`：等于它的原码。

`负数的反码`：将负数绝对值的原码，除符号位外，其它位按位取反。

- 数值 0 的反码表示有两种形式：[+0]~反~ = 0 0000000，[-0]~反~= 1 1111111。

### 补码

**反码也无法解决负数相加的问题。**例如：-1~反~ = 1110，-3~反~ = 1100，则 (-1~反~) + (-3~反~) = 1010，1010 的原码为 1101，即 -5，这很明显也是错误的。

`正数的补码`：等于它的原码。

`负数的补码`：等于它的反码 +1 或等于 $(2^{机器字长}-|负数|)$所得结果的原码。

- 数值 0 有唯一的编码：[+0]~补~ = 0 0000000，[-0]~补~ = 0 0000000。

**`计算机中均采用补码进行加减运算。`**

例如：若机器字长为 4，计算 6 - 2 。

解答：6~原~ = 0110 ---> 6~反~ = 0110 ---> 6~补~ = 0110，-2~原~ = 1010 ---> -2~反~ = 1101 ---> -2~补~ = 1110，则 6~补~ + (-2~补~) = 0100，即结果是一个正数，正数的补码等于反码等于源码，也就是 6 - 2 = 4，结果正确。

>如果 2X 的补码是 90H，那么 X 的真值是（ ）。（2016 上半年试题)
>
>A. 56
>
>B. -56
>
>C. 72
>
>D. -72
>
>【答案】B
>
>【解析】**十六进制用符号 H 或者 0x 表示，每一位十六进制代表四位二进制。**十六进制数 90，转换为二进制数为 1001 0000，补码 1001 0000 对应的反码为 1000 1111，再对应原码为 1111 0000，即 -112，因为 2X = -112，所以 X = -56。
>
>
>
>计算机系统中采用补码表示有符号的数值，（ ）。（2022 下半年试题）
>
>A. 可以保持加法和减法运算过程与手工运算方式一致
>
>B. 可以提高运算过程和结果的精准程度
>
>C. 可以提高加法和减法运算的速度
>
>D. 可以将减法运算转换为加法运算从而简化运算器的设计
>
>【答案】D
>
>
>
>原码表示法和补码表示法是计算机中用于表示数据的两种编码方法，在计算机系统中常采用补码来表示和运算数据，原因是采用补码可以（ ）。（2011 上半年试题）
>
>A. 保证运算过程与手工运算方法保持一致
>
>B. 简化计算机运算部件的设计
>
>C. 提高数据的运算速度
>
>D. 提高数据的运算精度
>
>【答案】B

### 移码

`移码`：补码的符号位取反，移码的主要用途是表示浮点数的指数（阶码）。

|        | 正数                                                         | 负数                                                         |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `原码` | **最高位为符号位 0 表示正号，其他位存放该数的二进制的绝对值** | **最高位为符号位 1 表示负号，其他位存放该数的二进制的绝对值** |
| `反码` | **等于原码**                                                 | **按它的原码，除符号位外，按位取反**                         |
| `补码` | **等于原码**                                                 | **反码 +1 或等于 $(2^{机器字长}-|负数|)$~原~**               |
| `移码` | **补码的符号位取反**                                         | **补码的符号位取反**                                         |

### 浮点数

浮点数的表示形式：**N = 尾数 × 基数^阶码（指数）^**

- 二进制中，基数都是 2，十进制中，基数都是 10，其他进制类推。
- 尾数一般是一个小数，阶码一般是一个整数。例如：1.23 × 10^5^。

浮点数的表示格式：

| 数符             | 阶符             |
| ---------------- | ---------------- |
| 尾数（**补码**） | 阶码（**移码**） |

- `尾数`：**用补码表示，位数决定数的有效精度，位数越多精度越高。**
- `阶码`：**用移码表示，位数决定数的表示范围，位数越多范围越大。**
- 对阶时，小数向大数看齐。
- 对阶是通过较小数的尾数右移实现的。

>浮点数的表示分为阶和尾数两部分。两个浮点数相加时，需要先对阶，即（ ）（n 为阶差的绝对值）。（2018 上半年试题）
>
>A. 将大阶向小阶对齐，同时将尾数左移 n 位
>
>B. 将大阶向小阶对齐，同时将尾数右移 n 位
>
>C. 将小阶向大阶对齐，同时将尾数左移 n 位
>
>D. 将小阶向大阶对齐，同时将尾数右移 n 位
>
>【答案】D
>
>
>
>对于长度相同但格式不同的两种浮点数，假设前者阶码长、尾数短，后者阶码短、尾数长，其它规定都相同，则二者可以表示数值的范围和精度情况为（ ）。（2022 下半年试题）
>
>A. 二者可表示的数的范围和精度相同
>
>B. 前者所表示的数的范围更大且精度更高
>
>C. 前者所表示的数的范围更大但精度更低
>
>D. 前者所表示的数的范围更小但精度更高
>
>【答案】C

## 校验码

### 奇偶校验

`奇偶校验码`的编码方法是：由若干位有效信息的头部或者尾部，再加上一个二进制位（校验位）组成校验码。

- `奇校验`：整个校验码（有效信息位和校验位）中 "1" 的个数为奇数。
- `偶校验`：整个校验码（有效信息位和校验位）中 "1" 的个数为偶数。

**奇偶校验码只能纠错，不能纠错：**

- 如果有**奇数个位发生误码**，则奇偶性发生变化，**可以检查出误码，但不能纠错。**
- 如果有**偶数个位发生误码**，则奇偶性不发生变化，**不能检查出误码（也称漏检）。**

>给出编码 1001101 的奇校验码和偶校验码（ ）。
>
>A. 10011011，10011010
>
>B. 10011011，10011011
>
>C. 10011010，10011010
>
>D. 10011010，10011010
>
>【答案】A

### 模 2 除法

模 2 除法计算过程：

1. 被除数首位是几商就上几；
2. 异或运算；
3. 异或后首位一定是0，舍弃掉这个0首位；
4. 补末位（落数），再上商。

例如，1011 0010 000 模2 除 1100 1，过程如下：

<img src="./system-architect-sprint/image-20240316143512427.png" alt="image-20240316143512427" style="zoom:50%;" />

计算到最后，余数为 4 位数，小于被除数 5 位数，计算完成。

### 循环冗余校验 CRC

流程：

- 收发双方约定好一个生成多项式 G(x)；

- 发送方基于待发送的数据和生成多项式计算出差错检测码（冗余码），然后将其添加到待传输数据的后面一起传输；

- 接收方通过生成多项式来计算收到的数据是否产生了误码。

  ● 算法要求生成多项式必须包含最低次项

示例一，待发送的信息为 1010 01，生成多项式为 G(x) = x^3^ + x^2^ + 1，计算编码后的信息。

1. **构造被除数：在待发送信息后面，添加生成多项式最高次数个 0。**即：1010 0100 0。

2. **构造除数：生成多项式各项系数构成的比特串。**即：1101。

3. **做模二除法运算。**得到余数为 1。

   <img src="./system-architect-sprint/image-20240316162956463.png" alt="image-20240316162956463" style="zoom:50%;" />

4. **检查余数：余数的位数应与生成多项式最高次数相同，如果位数不够，则在余数前补 0 来凑足位数。**即：001。

5. 因此，编码后的信息为：${\color{red}1010 01}$${\color{green}00 1}$。

示例二，接收到的信息为 1011 0100 1，生成多项式为 G(x) = x^3^ + x^2^ + 1，判断传输是否有误码。

1. **构造被除数：接收到的信息就是被除数。**即：1011 0100 1。

2. **构造除数：生成多项式各项系数构成的比特串。**即：1101。

3. **做模二除法运算。**得到余数为 11。

   <img src="./system-architect-sprint/image-20240316164514276.png" alt="image-20240316164514276" style="zoom:50%;" />

4. **检查余数：余数为 0，传输过程无误码；余数不为 0，传输过程产生误码。**

5. 因此，传输过程产生了误码。

>在（ ）校验方法中，采用模 2 运算来构造校验位。（2019 上半年试题）
>
>A. 水平奇偶
>
>B. 垂直奇偶
>
>C. 海明码
>
>D. 循环冗余
>
>【答案】D

### 海明校验

**设数据位是 n 位，校验位是 k 位，则 n 和 k 必须满足以下关系：2^k^ － 1 >= n + k。**

海明码的编码规则如下：设 k 个校验位为 P~k~，P~k-1~，…，P~1~，n 个数据位为 D~n~，D~n-1~，…，D~1~，对应的海明码为 H~n+k~，H~n+k-1~，…，H~1~。

（1）校验码 P~i~ 要放在 2^i-1^ 的位置。

（2）海明码中的任何一位都是由若干个校验位来校验的。

（3）被校验的海明位的下标，**等于所有参与校验该位的校验位的下标之和**，而校验位由自身校验。

>待传送的信息为 1010，若采用海明校验，则奇校验规则下的海明码是（ ）。
>
>A. 0110 010
>
>B. 0110 011
>
>C. 1110 010
>
>D. 1110 011
>
>【答案】A
>
>【解析】
>
>1. 数据位 n 等于 4，根据校验位和数据位之间的关系，校验位 k 等于 3（2^k^ >= 5 + k），海明位一共为 4 + 3 = 7。
>
>2. 因为校验码放在 2^i-1^ 的位置，则数据位和校验位之间的位置关系为：P1，P2，D1，P3，D2，D3，D4。海明位与数据位和校验位的关系为：
>
>   <img src="./system-architect-sprint/image-20240316171625487.png" alt="image-20240316171625487" style="zoom:50%;" />
>
>3. 海明位下标与校验位下标关系表（注意，校验位的下标是该校验位在海明位对应的位置，满足 2^i^ 条件，i 是大于等于 0 的整数）：
>
>   <img src="./system-architect-sprint/image-20240316194130312.png" alt="image-20240316194130312" style="zoom:50%;" />
>
>4. 根据上表，得出校验位和数据位的对应关系，进而根据对应的数据位数据，求出奇/偶校验码规则下对应的海明码：
>
>   <img src="./system-architect-sprint/image-20240316194715914.png" alt="image-20240316194715914" style="zoom:50%;" />
>
>5. 根据计算出来的奇/偶校验码规则下对应的海明码，将海明码填到对应的位置：
>
>   <img src="./system-architect-sprint/image-20240316195033389.png" alt="image-20240316195033389" style="zoom:50%;" />
>
>6. 因此，奇校验规则下，传输的信息为 0110 010。如果是偶校验规则，传输的信息为 1011 010。

## 存储器

### 存储器的层次结构

<img src="./system-architect-sprint/image-20240316223537530.png" alt="image-20240316223537530" style="zoom: 33%;" />

>在程序的执行过程中，Cache 与主存的地址映射是由（ ）完成的。（2017 下半年试题）
>
>A. 操作系统
>
>B. 程序员调度
>
>C. 硬件自动
>
>D. 用户软件
>
>【答案】C

### 高速缓存 Cache

特点：

- Cache 位于 CPU 与主存之间。

- Cache 对程序员来说是透明的。

- 设置多级高速缓存 Cache 以提高命中率（访问主存的效率）。

- **使用 Cache 改善系统性能的依据是程序的局部性原理。**

  <img src="./system-architect-sprint/image-20240316224600952.png" alt="image-20240316224600952" style="zoom: 50%;" />

  - `时间局部性`：被引用过一次的存储器位置在未来会被多次引用，**主要体现是循环**。
  - `空间局部性`：如果一个存储器的位置被引用，那么将来它附近的位置也会被引用，**主要体现是顺序执行的过程**。

>在 CPU 内外常设置多级高速缓存 Cache 其主要目的是（ ）。（2019 下半年试题）
>
>A. 扩大主存的存储容量
>
>B. 提高 CPU 访问主存数据或指令的效率
>
>C. 扩大存储系统的容量
>
>D. 提高 CPU 访问外存储器的速度
>
>【答案】B

### Cache 的地址映像方法

<img src="./system-architect-sprint/image-20240316224752879.png" alt="image-20240316224752879" style="zoom:67%;" />

>Cache 的地址映像方式中，发生块冲突次数最小的是（ ）。（2015 年上半年）
>
>A. 全相联映像
>
>B. 组相联映像
>
>C. 直接映像
>
>D. 无法确定
>
>【答案】A

### Cache 替换算法

<img src="./system-architect-sprint/image-20240316225305221.png" alt="image-20240316225305221" style="zoom:67%;" />

>Cache 的替换算法中，（ ）算法计数器位数多，实现困难。
>
>A. FIFO
>
>B. LFU
>
>C. LRU
>
>D. RAND
>
>【答案】B

### 磁盘（外存储器）

<img src="./system-architect-sprint/image-20240316225631889.png" alt="image-20240316225631889" style="zoom:67%;" />

机械磁盘存在两组运动：

- 磁盘的**旋转运动**。
- 机械臂控制磁头**沿半经方向的直线运动**。

**存取时间 = 寻道时间 + 等待时间：**

- `寻道时间`：指磁头移动到磁道所需的时间。
- `等待时间`：等待读写的扇区转到磁头下方所用的时间。
- 相较于寻道时间和等待时间，数据写入磁盘的时间微不足道，因此存取时间只考虑寻道时间和等待时间。

>在磁盘调度管理中，通常（ ）。（2019 下半年试题）
>
>A. 先进行旋转调度，再进行移臂调度
>
>B. 在访问不同柱面的信息时，只需要进行旋转调度
>
>C. 先进行移臂调度，再进行旋转调度
>
>D. 在访问同一磁道的信息时，只需要进行移臂调度
>
>【答案】C

## 输入/输出技术

输入/输出技术，是指 CPU 控制主存与外设之间数据交互的过程。因为外设处理速度比主存慢很多，对于二者之间的平衡，常见的方式有：

- `直接程序控制`
  - 分为无条件传送和程序查询方式。
  - 降低了 CPU 的效率。
  - 对外部的突发事件无法做出实时响应。
- `程序中断方式`
  - 利用中断方式完成数据的输入/输出。
  - CPU 接到中断请求信号后，保存正在执行程序的现场。
  - 与程序控制方式相比，因为 CPU 无须等待而提高了效率。
- `DMA`
  - 在主存与 I/O 设备（外设）之间建立数据通路，进行数据的交换处理。
  - 在 DMA 传送过程中无须 CPU 的干预。
  - DMA 传送数据时要占用系统总线，此时，CPU 不能使用总线。
- `输入/输出处理机 (IOP)`
  - 分担了 CPU 的一部分功能，可以实现对外围设备的统一管理，完成外围设备与主存之间的数据传送。
  - 大大提高了 CPU 的工作效率，这种效率的提高是以增加更多的硬件为代价的。

>DMA 控制方式是在（ ）之间直接建立数据通路进行数据的交换处理。（2019 年上半年试题软设）
>
>A. CPU 与主存
>
>B. CPU 与外设
>
>C. 主存与外设
>
>D. 外设与外设
>
>【答案】C
>
>
>
>计算机运行过程中，CPU 需要与外设进行数据交换。采用（ ）控制技术时，CPU 与外设可并行工作。（2017 年下半年)
>
>A. 程序查询方式和中断方式
>
>B. 中断方式和 DMA 方式
>
>C. 程序查询方式和 DMA 方式
>
>D. 程序查询方式、中断方式和 DMA 方式
>
>【答案】B

## Flynn 分类法



## 本文参考

https://www.zhihu.com/education/training/course-detail/1748737088365821953（请支持正版）

## 声明

写作本文初衷是个人学习记录，鉴于本人学识有限，如有侵权或不当之处，请联系 [wdshfut@163.com](mailto:wdshfut@163.com)。