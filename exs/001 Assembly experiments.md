

# 汇编实验（一）

### 1.基础知识

##### 关于Debug的应用

- 什么是Debug？

  Debug是DOS、Windows都提供的实模式程序的调试工具，使用它可以查看CPU各种寄存器中的内容、内存的情况和在机器码级跟踪程序的运行。

  相关功能：

  - r命令查看、修改CPU寄存器的内容；
  - d命令查看内存中的内容；
  - e命令改写内存中的内容；
  - u命令将内存中的机器指令翻译成汇编指令；
  - t命令执行一条机器指令；
  - a命令以汇编指令的格式在内存中写入一条机器指令。

- 资源

下载DOSBox：

链接：https://pan.baidu.com/s/15aVlmYrGbkKhPKtPuaapoA 
提取码：lt59 

- 安装教程

  ```
  ![0-0](D:\Desktop\汇编实验\实验1\0-0.png)1.下载完后，进行解压。
  2.打开DOSBox0.74，进行安装（全选默认即可）
  3.将debug复制的任意盘根目录中。
  4.从DOSBox的安装路径中打开DOSBox，
  5.在DOSBox中输入mount c D:\然后回车（复制后debug所在的盘的根目录）
  6.输入c:然后回车
  7.然后输入debug，即可开始汇编之旅了~~
  ```

  打开如图：

![0-0](D:\Desktop\汇编实验\实验1\0-0.png)

### 2.实验任务

##### （1）使用Debug，将下面的程序段写入内存，逐条执行，观察每条指令后CPU中相关寄存器中内容的变化



| 机器码   | 汇编指令        |
| :------- | :-------------- |
| b8 20 4e | `mov ax, 4E20H`|
| 05 16 14 | `add ax, 1416H` |
| bb 00 20 |`mov bx, 2000H`   |
| 01 d8    |`add ax, bx `   |
| 89 c3    | `mov bx, ax`     |
| 01 d8    |`add ax, bx`    |
| b8 1a 00 | `mov ax, 001AH` |
| bb 26 00 | `mov bx, 0026H` |
| 00 d8    | `add al, bl ` |
| 00 dc    | `add ah, bl` |
| 00 c7    | `add bh, al ` |
| b4 00    | `mov ah, 0` |
| 00 d8    | `add al, bl` |
| 04 9c    | `add al,9CH` |

**提示：可用E命令和A命令以两种方式将指令写入内存。注意用T命令执行时，CS：IP的指向。**

##### [Answer]：

- input Assembly Language (汇编指令) 

  ​	{我使用 a 的指令，也可以使用 E 命令。

  ​	a 的作用：直接输入汇编指令}

- 利用a指令，输入汇编指令

- 利用**rip 、rcs命令**修改**段地址、偏移地址**

![1-2](D:\Desktop\汇编实验\实验1\1-2.png)

- 利用r命令，查看当前各详细参数。
- 然后利用t命令，依次执行汇编指令。观察寄存器以及CS：IP的指向变化

![1-3](D:\Desktop\汇编实验\实验1\1-3.png)





| 机器码   | 汇编指令        | 寄存器（ax，bx） | CS：IP |
| :------- | :-------------- | ---------------- | ------ |
| b8 20 4e | `mov ax, 4E20H` |                  |        |
| 05 16 14 | `add ax, 1416H` |                  |        |
| bb 00 20 | `mov bx, 2000H` |                  |        |
| 01 d8    | `add ax, bx `   |                  |        |
| 89 c3    | `mov bx, ax`    |                  |        |
| 01 d8    | `add ax, bx`    |                  |        |
| b8 1a 00 | `mov ax, 001AH` |                  |        |
| bb 26 00 | `mov bx, 0026H` |                  |        |
| 00 d8    | `add al, bl `   |                  |        |
| 00 dc    | `add ah, bl`    |                  |        |
| 00 c7    | `add bh, al `   |                  |        |
| b4 00    | `mov ah, 0`     |                  |        |
| 00 d8    | `add al, bl`    |                  |        |
| 04 9c    | `add al,9CH`    |                  |        |



##### （2）将下面3条指令写入从2000:0开始的内存单元中，利用这3条指令计算2的8 次方;

**指令：**

```
mov ax 1,

add ax, ax

jmp 2000:0003
```

##### [Answer]

![2-1](D:\Desktop\assembly_ language_ex\ex1\2-1.png)

![2-2](D:\Desktop\assembly_ language_ex\ex1\2-2.png)

![2-3](D:\Desktop\assembly_ language_ex\ex1\2-3.png)

![2-4](D:\Desktop\assembly_ language_ex\ex1\2-4.png)

![2-5](D:\Desktop\assembly_ language_ex\ex1\2-5.png)

![2-6](D:\Desktop\assembly_ language_ex\ex1\2-6.png)

- 首先用rcs、rip指令修改CS：IP
- 用A指令输入相关汇编指令。

**[conclude]** 

- 先执行第一条指令
- 重复执行8次（2、3指令）即：得到了2的8次方



##### （3）查看内存中的内容。

​	PC机主板上的ROM中写有一个生产日期，在内存FFF00H~FFFFFH 的某几个单元中，请找到这个生产日期并试图改变它。

提示：如果读者对实验的结果感到疑惑，请仔细阅读教材。

![3-0001](D:\Desktop\assembly_ language_ex\ex1\3-0001.png)

##### [Answer]：

可以查看，但是由于DOS的性质，好像无法修改



##### （4）向内存从B8100H开始的单元中填写数据，如：

​	-e B810 : 0000 01 01 02 02 03 03 04 04 

请读者先填写不同的数据，观察产生的现象：再改变填写的地址，观察产生的现象。

提示：如果读者对实验的结果感到疑惑，请仔细阅读第一章中的1.15节。

##### [answer]

无法修改。