---
comments: true
---

# NEMU计算机系统基础实践



## PA0 实验前的准备

![c1fee2a3453712587022ce61b078616](C:\Users\10648\Documents\WeChat Files\wxid_zzpw95f4t49e22\FileStorage\Temp\c1fee2a3453712587022ce61b078616.png)

实验手册：

[PA0-实验前的准备.pdf](file:///C:/Users/10648/AppData/Local/Temp/c27e642b-b9e7-4dc4-9266-ed95ec4606f3_实验指导书.zip.6f3/实验指导书/PA0-实验前的准备.pdf)

**注：版本控制**

虽然 git 可以跟踪你的开发痕迹，但这些痕迹记录还不足以支撑你的开发过程。每当你成功完成一个子任务，你都可以利用 git 将这个阶段性版本提交至本地仓库，这就是一种简单的版本控制。上述工作需要你手工完成，命令如下：

> git add . 

> git commit --allow-empty 

输入“commit”命令后会弹出已设定的编辑器窗口（例如，vim），你可以在其中**输入对当前版本的描述信息**，以便于今后查找。如果版本描述信息比较简单， 也可以在“commit”命令后使用-m 选项，直接输入描述信息。此外，“--allowempty”是一个可选的选项。因为，有些时候你对代码的改变已经被 git 系统自 动记录了，此时如果不使用“--allow-empty”选项，git 是无法完成本地提交 的。如果最终提交成功，通过如下“log”命令你可以找到使用你的学号和姓名 标注的日志信息。

> git log

 如果你想在众多日志信息中定位你手工提交的信息，可以在 git 的“log”命令 中添加“author”选项。更多使用细节请阅读附件 4 或百度查询。

**注： 提交git**

> git add .
>
> git commit -m “3023244358”

**注： git版本回退**

> `git reset --hard HEAD^`    // 为先回退到上一个已推送版本
>
> `git reset --hard origin/master`   // 进行已提交，但未推送的版本回退
>
> `git reset --hard 710ae83`   // 其中`710ae83`是用`git log`查看的版本号

**注：编译、运行 NEMU**

 NEMU 实现的是一台基于 IA-32 指令集的虚拟机，在终端中输入如下命令 完成 NEMU 的编译和运行：

> make 
>
> make clean   (*********重要**********)
>
> make run

**注： 打包压缩**

>`make submit`      // 打包所在路径的整个项目文件
>
>`find .. -name "3023244358.zip"`    //在上一级目录中查找压缩包

**注： 删除之前的压缩包**

> `cd ..  `  // 生成的压缩包在上一级目录
>
> `rm 3023244358.zip  ` 



问题：

#### q1：make指令报错

报错种类：

```asm
fatal error : readline/readline.h : No such file or directory…
Entering emergency mode, exit the shell to continue. Type “journalctl” to view systems logs…
```

ans1：更新[软件包](https://so.csdn.net/so/search?q=软件包&spm=1001.2101.3001.7020)列表

> sudo apt update

使用以下命令安装gcc编译器：

> sudo apt install build-essential

使用命令来安装GCC的开发环境

> sudo apt-get install build-essential
>
> sudo apt-get install libreadline-dev	



#### q2：关于git：如何将clone下来的项目上传到自己的仓库

将clone下来的项目上传到自己的仓库：

1.clone你需要的项目

> [git](https://so.csdn.net/so/search?q=git&spm=1001.2101.3001.7020) clone xxx

2.进入项目目录

> cd xxx

3.删除原有的git信息，有问题一直回车

> rm -r .git

4.初始化git

> git init

5.讲本地代码添加到仓库

> git add .
> git commit -m “xxx”

6.在git官网上新建一个项目，注意不要生成README文件
7.关联远程库

> git remote add origin 远程库地址

8.提交代码

> * git push --set-upstream origin master    

##### 报错

##### error: failed to push some refs to 'https://gitee.com/indexdog/jz-lab'

原来使用的提交命令是git push -u origin 分支名

不妨尝试一下使用覆盖提交的方式

git push -f origin 分支名

其中“-f”是覆盖提交的参数。

> git push -f origin master
>
> 

## PA1 简易调试器

叠甲：参考博客

https://blog.csdn.net/qq_45655405/article/details/108941025

https://www.cnblogs.com/grapefruit-cat/p/17153407.html

https://blog.csdn.net/weixin_43877657/article/details/109068930



实验手册：

[PA1-简易调试器.pdf](file:///C:/Users/10648/AppData/Local/Temp/bdb5f9b3-8d49-4c62-8f26-bab2b5fae8c6_实验指导书.zip.8c6/实验指导书/PA1-简易调试器.pdf)

### 阶段一



##### 思考题 1：opcode_table 到底是一个什么类型的数组？

**opcode_table**数组为 **helper_fun** 类型，在同一个文件中看到 **helper_fun** 的定义为：
![image-20240827145007815](C:\Users\10648\AppData\Roaming\Typora\typora-user-images\image-20240827145007815.png)

此处 **typedef** 的功能是定义新的 **helper_fun** 类型，并定义这种类型为指向某种函数的指针，这种函数以一个 **swaddr_t** 为参数并返回 **int** 类型。因此，**opcode_table** 数组是一个函数指针数组。



##### 思考题 2：在 cmd_c()函数中, 调用 cpu_exec()的时候传入了参数-1 , 你知道为什么吗?

n是无符号整型，所以-1就是无符号最大的数字，那么函数里的for循环可以执行最大次，以保证所有数据的有效。



#### nemu命令语法

![image-20240828092438677](C:\Users\10648\AppData\Roaming\Typora\typora-user-images\image-20240828092438677.png)

#### nemu 目录下的源文件组织

![image-20240828100241826](C:\Users\10648\AppData\Roaming\Typora\typora-user-images\image-20240828100241826.png)

#### 必做任务 1：实现正确的寄存器结构体

NEMU 中通用寄存器为：32位寄存器；16位寄存器；8 位寄存器

但它们在物理上并不是相互独立的, 例如 EAX 的低 16 位是 AX , 而 AX 又分成 AH 和 AL。

我们需要了解Struct与Union的概念，保证`gpr[i]`对应第`i`个寄存器即可。

> Struct与Union主要有以下区别:
>
> 1）在任何同一时刻, union中只存放了一个被选中的成员, 而struct的所有成员都存在。在struct中，各成员都占有自己的内存空间，它们是同时存在的。一个struct变量的总长度等于所有成员长度之和。在Union中，所有成员不能同时占用它的内存空间，它们不能同时存在。Union变量的长度等于最长的成员的长度。
>
> 2）对于union的不同成员赋值, 将会对其它成员重写, 原来成员的值就不存在了, 而对于struct的不同成员赋值是互不影响的。



代码修改：` NEMU/nemu/include/cpu/reg.h`

这是一个用C语言定义的结构体类型，用于描述一个模拟的CPU状态。以下是逐行解释：

```asm
typedef struct {
```

- `typedef`：这是C语言中的关键字，用于定义一个新的类型别名。在这里，它定义了一个名为`CPU_state`的新类型。
- `struct`：关键字`struct`表示这是一个结构体类型。

```asm
union {
```

- `union`：这里定义了一个联合体（union），在C语言中，联合体中的所有成员共享相同的内存空间，也就是说它们是互斥的，只能存储一个值。

```asm
union {
			uint32_t _32;
			uint16_t _16;
			uint8_t _8[2];
		} gpr[8];
```

- 内部的这个联合体表示通用寄存器（GPRs）。每个通用寄存器可以是32位（`_32`）、16位（`_16`）或是两个8位（`_8[2]`）的数组。
- `gpr[8]`：这个定义表示有8个通用寄存器，它们共享相同的内存空间，每个寄存器可以存储不同大小的数据。

```asm
struct {
		uint32_t eax, ecx, edx, ebx, esp, ebp, esi, edi;
    };
```

- 这里的结构体包含了8个32位的寄存器名，分别是`eax`, `ecx`, `edx`, `ebx`, `esp`, `ebp`, `esi`, 和`edi`。这些寄存器是常见的x86架构中的寄存器名称。
- 这8个寄存器与前面的`gpr`数组是一一对应的，两个表示方式是等价的，只是提供了不同的访问方式。

```asm
	};
```

- 结束第一个联合体的定义。

```asm
    /* Do NOT change the order of the GPRs' definitions. */
```

- 注释提示不要更改GPR定义的顺序，因为代码逻辑依赖于当前顺序。

```asm
swaddr_t eip;
```

- `eip`是结构体中的一个成员，表示当前的指令指针（指向下一条要执行的指令）。`swaddr_t`是一个类型别名，通常表示软件地址。

```asm
union {
		struct {
			uint32_t CF		:1;
			uint32_t pad0	:1;
			uint32_t PF		:1;
			uint32_t pad1	:1;
			uint32_t AF		:1;
			uint32_t pad2	:1;
			uint32_t ZF		:1;
			uint32_t SF		:1;
			uint32_t TF		:1;
			uint32_t IF		:1;
			uint32_t DF		:1;
			uint32_t OF		:1;
			uint32_t IOPL	:2;
			uint32_t NT		:1;
			uint32_t pad3	:1;
			uint16_t pad4;
		};
		uint32_t val;
	} eflags;
```

- 这里是另一个联合体，用于表示CPU的状态标志寄存器（eflags）。
- 内部的结构体将标志寄存器分解为多个标志位，例如CF（进位标志）、PF（奇偶标志）、ZF（零标志）等，每个标志位用1位（bit）表示。
- `pad`字段用于填充位，以确保整个结构的对齐和大小符合要求。
- `val`字段提供了一种可以一次性访问整个32位标志寄存器的方式。

```asm
} CPU_state;
```

- 最后，结束结构体的定义，并通过`typedef`为其取名`CPU_state`。这个结构体可以用来描述并存储CPU的当前状态。

#### 必做任务 2：实现单步执行、打印寄存器、扫描内存

- 单步执行

单步执行的格式为si [N]，程序单步执行N条指令后暂停, 当N没有给出时, 缺省为默认为1。根据单步执行的说明得出解题步骤：

1）传入cmd_si()函数的参数为字符串，现在需要利用一些方法将其分解为两部分，分别为“si （空格）”和“N”(N是字符串类型的数字），N的部分存到字符串arg中，此过程中需要用到strtok()库函数，[查阅资料](https://www.runoob.com/cprogramming/c-function-strtok.html)知道：

> strtok( ) 的使用
> C 库函数 char *strtok(char *str, const char *delim) 分解字符串 str 为一组字符串，delim 为分隔符。

2）根据字符串arg来判断需要执行的指令数 i，需要使用sscanf()库函数，将字符串arg改为int型的数字 i，[查阅资料](https://www.runoob.com/cprogramming/c-function-sscanf.html)知道：

> sscanf( ) 的使用
> C 库函数 int sscanf(const char *str, const char *format, …) 从字符串读取格式化输入。
> str – 这是 C 字符串，是函数检索数据的源。
> format – 这是 C 字符串，包含了以下各项中的一个或多个：空格字符、非空格字符和format 说明符。

① 若arg为NULL，默认 i = 1
② 若 i < -1, 提示输入错误
③ 若 i >= -1, 调用次 cpu_exec(steps)

代码修改：`/home/camelu1/NEMU2021/nemu/src/monitor/debug/ui.c`

```c
static int cmd_si(char *args)
{
	char *arg = strtok(NULL, " "); //使用 strtok 函数从 args 中获取下一个参数。NULL 表示继续上一次的分割操作
	int steps = 0;
	if (arg == NULL) //默认为 1
	{
		cpu_exec(1);
		return 0;
	}
	sscanf(arg, "%d", &steps); //使用 sscanf 从 arg 字符串中读取整数值，存储到 steps 变量中
	if (steps < -1) //检查是否有效
	{
		printf("Error, N is an integer greater than or equal to -1\n");
		return 0;
	}
	cpu_exec(steps); //调用 cpu_exec 函数，传入 steps 参数，执行指定数量的 CPU 操作

	return 0;
}
```

**遭遇报错：error: ‘cmd_si’ defined but not used [-Werror=unused-function]**

这个错误信息表明在编译过程中，函数 `cmd_si` 被定义但未使用，导致编译器发出警告，并且由于 `-Werror` 选项，该警告被视为错误，导致编译失败。

**解决方法**

在同文件`static struct`下加入`{"si", "Single step execution", cmd_si}`描述

```c
static struct {
	char *name;
	char *description;
	int (*handler) (char *);
} cmd_table [] = {
	{ "help", "Display informations about all supported commands", cmd_help },
	{ "c", "Continue the execution of the program", cmd_c },
	{ "q", "Exit NEMU", cmd_q },

	/* TODO: Add more commands */
	{"si", "Single step execution", cmd_si}

};
```

**修改最大步数** 

阅读`cmd_c`，可知程序运行在`cpu_exec()`函数中，`-1`转成无符号数即为最大能表示的数，所以程序会全部执行完。我们只需要把`-1`改成`si`后面的参数即可。

在`/home/camelu1/NEMU2021/nemu/src/monitor/cpu-exec.c`文件中 `\#define MAX_INSTR_TO_PRINT 10` 中的10改为`-1`就可以了

- 打印寄存器

打印程序状态的命令格式为`info SUBCMD` ，当SUBCMD为 r 时`info r`打印印寄存器状态，只需要printf每一个寄存器的状态。

代码修改：`/home/camelu1/NEMU2021/nemu/src/monitor/debug/ui.c`

```c
static int cmd_info(char *args) {
	if (args[0] == 'r') {
		int i;
		for (i = R_EAX; i <= R_EDI ; i++) { //使用 for 循环，从 R_EAX 到 R_EDI（假设这两个常量定义了寄存器的范围），遍历所有相关的寄存器。
			printf("$%s\t0x%08x\t%d\n", regsl[i], reg_l(i), reg_l(i));
			//regsl[i] 是寄存器名称，reg_l(i) 是一个函数调用，用于获取寄存器的值，格式为 0x 开头的 8 位十六进制数和十进制数
		}
		printf("$eip\t0x%08x\t%d\n", cpu.eip, cpu.eip);//***********
		//打印当前的指令指针 eip 的值，格式同样为 0x 开头的 8 位十六进制数和十进制数

		//$eip 字符串常量，表示输出的内容前缀，指示这是指令指针的值
        //\t 转义字符，表示输出一个制表符，用于格式化输出，使不同部分之间有一定的间隔
        //0x%08x 0x:十六进制 %08x：% 开头表示格式化输出，08 表示输出至少 8 位，不足的部分用零填充，x 表示以小写十六进制格式输出。
        //%d 格式说明符，表示以十进制格式输出接下来的数字
        //\n 转义字符，表示输出一个换行符，结束当前行的输出
        //cpu.eip 结构体成员，表示当前的指令指针值。它被用作 0x%08x 和 %d 的参数，分别输出其十六进制和十进制值
	}
	return 0;
}
```

添加描述

```c
{"info", "r to print register values\n       w to show watch point state", cmd_info}
```

- 扫描内存

内存扫描命令的格式为x N EXPR，N表示扫描长度，EXPR为起始内存。因此得出**解题步骤**：

1）传入`cmd_x()`函数的参数为字符串，需要利用`strtok()`函数分别得到 N 和 EXPR 部分的字符串，再利用`sscanf()`函数将字符串 N 转化为十进制整型数 len，把字符串EXPR转化为十六进制的数address。
2）任务中要求以16进制 形式输出连续的N个4字节，因此，将address和4传入`lnaddr_read`函数就可以得到，再用for循环循环len次，每次循环时起始地址加4,就可以实现内存的扫描。

```c
static int cmd_x(char *args) {
    char *N = strtok(NULL, " ");  // 分割字符串，读取字节数
    char *EXPR = strtok(NULL, " ");  // 继续分割，内存地址的表达式
    int len;  // 存储读取的字节数
    lnaddr_t address; // 存储要读取的内存地址 

    sscanf(N, "%d", &len);  // 从字符串 N 中读取整数值，存储到 len 变量中
    sscanf(EXPR, "%x", &address);  // 从字符串 EXPR 中读取十六进制地址，存储到 address 中

    int i;
    for (i = 0; i < len; i++) {  
        if (i % 4 == 0) {  // 每 4 个值前打印地址
            printf("0x%08x: ", address);
        }
        
        printf("0x%08x ", lnaddr_read(address, 4)); 
        // 调用 lnaddr_read 函数，从当前 address 读取 4 字节数据，并以 8 位十六进制格式打印 
        address += 4;  // 更新地址

        if ((i + 1) % 4 == 0) printf("\n");  // 每 4 个值换行
    }  
    if (len % 4 != 0) printf("\n");  // 如果最后一行不满 4 个值，换行
    return 0;  
}

```

### 阶段二

#### 必做任务 3：实现算术表达式的词法分析

`/home/camelu1/NEMU2021/nemu/src/monitor/debug/expr.c`

修改代码：

```c
#include "nemu.h"

/* We use the POSIX regex functions to process regular expressions.
 * Type 'man regex' for more information about POSIX regex functions.
 */
#include <sys/types.h>
#include <regex.h>

enum {
    NOTYPE = 256, EQ, NUMBER, REGISTER, HNUMBER, NEQ, AND, OR, POINTER, MINUS,

    /* TODO: Add more token types */

};

static struct rule {
    char *regex;
    int token_type;
    int priority;
} rules[] = {

    /* TODO: Add more rules.
     * Pay attention to the precedence level of different rules.
     */

    {" +",    NOTYPE, 0},                // spaces
    {"\\b[0-9]{1,31}\\b",NUMBER,0}, // number
    {"\\|\\|",OR,1},                // or
    {"&&",AND,2},                   // and
    {"==", EQ, 3},                  // equal
    {"!=", NEQ, 3},                 // not equal
    {"\\+", '+', 4},                // plus
    {"-", '-', 4},                  // sub
    {"\\*", '*', 5},                // multiples
    {"/", '/', 5},                  // divide
    {"!",'!',6},                    // not
    {"\\(", '(', 7},
    {"\\)", ')', 7},                // braces
    {"\\b0[xX][0-9a-fA-F]{1,31}\\b",HNUMBER,0},        // hex number
    {"\\$[a-zA-Z]{2,3}",REGISTER,0},                  // register
};

#define NR_REGEX (sizeof(rules) / sizeof(rules[0]) )

static regex_t re[NR_REGEX];//宏定义表示正则表达式的数量

/* Rules are used for many times.
 * Therefore we compile them only once before any usage.
 */
void init_regex() {//编译所有的正则表达式并存储到re[]数组中，如果编译失败，会输出错误信息并中止程序
    int i;
    char error_msg[128];
    int ret;

    for(i = 0; i < NR_REGEX; i ++) {
        ret = regcomp(&re[i], rules[i].regex, REG_EXTENDED);
        if(ret != 0) {
            regerror(ret, &re[i], error_msg, 128);
            Assert(ret == 0, "regex compilation failed: %s\n%s", error_msg, rules[i].regex);
        }
    }
}

typedef struct token {
    int type;
    int priority;
    char str[32];
} Token;

Token tokens[32];
int nr_token;

static bool make_token(char *e) {//依次匹配正则表达式来识别输入字符串中的标记并存储到tokens[]数组中
    int position = 0;
    int i;
    regmatch_t pmatch;
    
    nr_token = 0;

    while(e[position] != '\0') {
        /* Try all rules one by one. */
        for(i = 0; i < NR_REGEX; i ++) {
            if(regexec(&re[i], e + position, 1, &pmatch, 0) == 0 && pmatch.rm_so == 0) {
                char *substr_start = e + position;
                int substr_len = pmatch.rm_eo;

                //Log("match rules[%d] = \"%s\" at position %d with len %d: %.*s", i, rules[i].regex, position, substr_len, substr_len, substr_start);

                /* TODO: Now a new token is recognized with rules[i]. Add codes
                 * to record the token in the array `tokens'. For certain types
                 * of tokens, some extra actions should be performed.
                 */
                switch(rules[i].token_type) {
                    case NOTYPE: break;
                    case REGISTER: {
                        tokens[nr_token].type = rules[i].token_type;
                        tokens[nr_token].priority = rules[i].priority;
                        strncpy(tokens[nr_token].str, substr_start + 1, substr_len - 1);
                        tokens[nr_token].str[substr_len-1] = '\0';
                        nr_token ++;
                        
                        break;
                    } // REGISTERS recorded as "[register name]\0", lost of first'$'
                    default:{
                        tokens[nr_token].type = rules[i].token_type;
                        tokens[nr_token].priority = rules[i].priority;
                        strncpy(tokens[nr_token].str, substr_start, substr_len);
                        tokens[nr_token].str[substr_len] = '\0';
                        nr_token ++;

                        break;
                    } // Normal types
                }
                position += substr_len;
                break;
            }
        }
        if(i == NR_REGEX) {
            printf("no match at position %d\n%s\n%*.s^\n", position, e, position, "");
            return false;
        }
    }
    
    return true;
}

bool check_parentness(uint32_t lp, uint32_t rp){//括号匹配函数
    if(tokens[lp].type == '(' && tokens[rp].type == ')'){
        int lbn = 0, rbn = 0;
        int i = lp + 1;
        for(; i < rp; i ++){
            if(tokens[i].type == '(') lbn ++;
            if(tokens[i].type == ')') rbn ++;
            if(rbn > lbn) return false;
        }
        
        return true;
    }
    
    else return false;
}

uint32_t make_dop(int lp, int rp){//找到当前表达式中优先级最低的操作符
    int i, j;
    int dop = lp;
    int min_priority = 10;
    for(i = lp; i <= rp; i ++){
        if (tokens[i].type == NUMBER || tokens[i].type == HNUMBER || tokens[i].type == REGISTER)
                    continue;
        int cnt = 0;//跟踪括号的匹配情况
        bool key = true;//标记当前操作符是否在括号内
        for (j = i - 1; j >= lp ;j --){
            if (tokens[j].type == '(' && !cnt){key = false;break;}
            if (tokens[j].type == '(')cnt --;
            if (tokens[j].type == ')')cnt ++;
        }
            if (!key)continue;
            if (tokens[i].priority <= min_priority){min_priority = tokens[i].priority;dop = i;}
        //如果当前操作符的优先级tokens[i].priority小于或等于当前记录的最低优先级min_priority，更新min_priority并将当前操作符的位置i记录到dop中，作为新的分割点
    }
    
    return dop;
}

uint32_t eval(int lp, int rp){//递归求值
    if(lp > rp) { Assert (lp > rp, "Wrong expression!\n"); return 0;}
    
    else if (lp == rp){//表达式只有一个标记，即单一的数字、寄存器或其他类型
        uint32_t num = 0;
        if(tokens[lp].type == NUMBER)
            sscanf(tokens[lp].str, "%d", &num);//通过 sscanf 将字符串转换为整数
        else if (tokens[lp].type == HNUMBER)
            sscanf(tokens[lp].str, "%x", &num);//通过 sscanf 以十六进制形式将字符串转换为整数
        else if (tokens[lp].type == REGISTER){
            if(strlen(tokens[lp].str) == 3){//函数检查寄存器名的长度
                int i;
                for(i = R_EAX; i <= R_EDI; i++){//如果是3个字符，将其与32位寄存器名列表regsl中的寄存器名称逐一比较，找到匹配项后将相应寄存器的值赋值给num
                    if(strcmp(tokens[lp].str, regsl[i]) == 0) {num = reg_l(i);  break;}
                }
                if( i > R_EDI && strcmp(tokens[lp].str, "eip") == 0) num = cpu.eip;
                    else Assert(1, "No such register, you may check for your spellings");
            }
            else if(strlen(tokens[lp].str) == 2){//如果寄存器名称为2个字符，进一步检查第二个字符的类型
                int i;
                if(tokens[lp].str[1] == 'x' || tokens[lp].str[1] == 'i' || tokens[lp].str[1] == 'p'){//如果第二个字符是x、i或p，则匹配16位寄存器列表regsw中的寄存器，找到匹配项后将相应寄存器的值赋值给num
                    for(i = R_AX; i <= R_DI; i ++){
                        if(strcmp(tokens[lp].str, regsw[i]) == 0) {num = reg_w(i);  break;}
                        else Assert(1, "No such register, you may check for your spellings");
                    }
                }
                else if(tokens[lp].str[1] == 'h' || tokens[lp].str[1] == 'l'){
                    //如果第二个字符是h或l，则匹配8位寄存器列表regsb中的寄存器，找到匹配项后将相应寄存器的值赋值给num。
                    for(i = R_AL; i <= R_BH; i ++){
                        if(strcmp(tokens[lp].str, regsb[i]) == 0) {num = reg_b(i);  break;}
                        else Assert(1, "No such register, you may check for your spellings");
                    }
                }
            }
            else assert(1);
        }
        
        return num;
    }
    
    else if(check_parentness(lp, rp) == 1){
        //如果lp和rp之间的子表达式被括号包围，检查是否括号匹配
        return eval(lp + 1, rp - 1);//递归调用eval求值
    }
    else{
        uint32_t dop;
        dop = make_dop(lp, rp);
        if(dop == lp || tokens[dop].type == MINUS || tokens[dop].type == POINTER
                || tokens[dop].type == '!'){
            //若dop位操作符是单目运算符
            int val;
            val = eval(lp + 1, rp);//则递归求解右侧的子表达式，即从lp+1到rp
            switch (tokens[dop].type) {
                case MINUS: return -val;
                case POINTER: return swaddr_read(val, 4);
                case '!': return !val;
                default: Assert(1, "Wrong expression!");
            }
        }
        ////若dop位操作符是双目运算符
        uint32_t val1, val2;
        val1 = eval(lp, dop - 1); 
        val2 = eval(dop + 1, rp);
        
        switch (tokens[dop].type) {
            case '+': return val1 + val2;
            case '-': return val1 - val2;
            case '*': return val1 * val2;
            case '/': return val1 / val2;
            case OR: return val1 || val2;
            case AND: return val1 && val2;
            case EQ: return val1 == val2;
            case NEQ: return val1 != val2;
            default: Assert(1, "Wrong expression!");
        }
    }
    
    return 0;
}

uint32_t expr(char *e, bool *success) {
    //e：待计算的字符串表达式
    //success：一个布尔指针 指示表达式求值是否成功
    if(!make_token(e)) {
        //词法分析，将其分解成tokens
        *success = false;
        return 0;
    }

    /* TODO: Insert codes to evaluate the expression. */
    int i = 0;
    for (i = 0;i < nr_token; i ++) {//遍历所有tokens，并进行一些特殊处理
        if (tokens[i].type == '*' && (i == 0 || (tokens[i - 1].type != NUMBER && tokens[i - 1].type != HNUMBER && tokens[i - 1].type != REGISTER && tokens[i - 1].type !=')'))) {
            //解引用操作
            tokens[i].type = POINTER;
                tokens[i].priority = 6;//设置其优先级为6
            }
        if (tokens[i].type == '-' && (i == 0 || (tokens[i - 1].type != NUMBER && tokens[i - 1].type != HNUMBER && tokens[i - 1].type != REGISTER && tokens[i - 1].type !=')'))) {
            //取负号操作
                tokens[i].type = MINUS;
                tokens[i].priority = 6;
            }
    }
    *success = true;
    
    return eval(0, nr_token - 1);
}


```



##### 思考题 2：框架代码中定义 wp_pool 等变量的时候使用了关键字 static，static 在此处 的含义是什么? 为什么要在此处使用它?

`wp_pool` 是全局数据结构，当变量被声明为 `static` 时，它的生命周期会持续整个程序运行期间。这意味着即使在函数执行完毕后，该变量仍然存在于内存中，而不是在函数调用结束后被销毁，提高了代码的安全性和可维护性

`static` 还限制了变量的作用域。对于在函数内部声明的 `static` 变量，它只能在该函数内访问，外部代码无法直接访问。这有助于避免命名冲突和意外修改，确保这些变量的使用是局部的，增强了封装性

### 阶段三

#### 必做任务 6：实现监视点池的管理

添加代码`/home/camelu1/NEMU2021/nemu/src/monitor/cpu-exec.c`

```c
bool jug = check_wp();//判断是否有监视点条件被触发
		if ( !jug ) nemu_state = STOP;//当 check_wp() 检查失败或没有满足特定条件时，停止操作
```



添加函数`/home/camelu1/NEMU2021/nemu/src/monitor/debug/watchpoint.c`

```c
void init_wp_pool() {
    int i;
    for(i = 0; i < NR_WP; i ++) {
        wp_pool[i].NO = i;  // 为每个监视点分配一个编号
        wp_pool[i].next = &wp_pool[i + 1];  // 将当前监视点的下一个指针指向下一个监视点
    }
    wp_pool[NR_WP - 1].next = NULL;  // 最后一个监视点的下一个指针设为 NULL

    head = NULL;  // 初始化监视点链表头为 NULL
    free_ = wp_pool;  // 初始化空闲监视点指针指向监视点池
}


WP* new_wp(char * exp){
    assert(free_ != NULL);  // 确保有可用的监视点
    WP *temp = free_;  // 获取当前空闲的监视点
    free_ = free_->next;  // 更新空闲指针到下一个监视点
    temp->next = NULL;  // 初始化新监视点的下一个指针为 NULL

    bool success = false;
    strcpy(temp->exp, exp);  // 复制表达式到监视点
    temp->value = expr(temp->exp, &success);  // 计算表达式的初始值
    assert(success);  // 确保表达式计算成功

    if(head == NULL)  // 如果链表为空
        head = temp;  // 将新监视点设置为头
    else {
        WP *p = head;
        while(p->next)  // 遍历到链表的末尾
            p = p->next;
        p->next = temp;  // 将新监视点添加到链表末尾
    }
    return temp;  // 返回新创建的监视点
}


int free_wp(WP *wp){
    if(wp == NULL)  // 检查输入是否为 NULL
        printf("Input something!\n");
    if(wp == head)  // 如果要释放的监视点是头
        head = head->next;  // 更新头指针
    else {
        WP *p = head;
        while(p->next != wp)  // 遍历链表找到要释放的监视点
            p = p->next;
        if(p == NULL)  // 如果没有找到
            return 0;  // 返回失败
        p->next = wp->next;  // 从链表中移除监视点
    }
    wp->next = free_;  // 将释放的监视点放回空闲链表
    free_ = wp;  // 更新空闲指针
    return 1;  // 返回成功
}


bool check_wp(){
    WP* wp = head;  // 从头开始遍历监视点链表
    bool suc, key;
    key = true;  // 初始化检查标志为 true
    while(wp != NULL) {
        int val = expr(wp->args, &suc);  // 计算当前监视点的表达式值
        if(!suc) assert(1);  // 如果计算失败，触发断言
        if(wp->val != val) {  // 如果值发生变化
            key = false;  // 设置检查标志为 false
            printf("Hint breakpoint %d at address 0x%08x\n", wp->NO, cpu.eip);
            printf("Watchpoint %d: %s\n", wp->NO, wp->args);
            printf("Old value = %d\n", wp->val);
            printf("New value = %d\n", val);
            wp->val = val;  // 更新监视点的值
        }
        wp = wp->next;  // 移动到下一个监视点
    }
    
    return key;  // 返回检查结果
}


void delete_wp(int num){
    WP *p = head;
    while(p->next && p->NO != num)  // 遍历找到要删除的监视点
        p = p->next;
    if(p->NO == num)  // 如果找到监视点
        free_wp(p);  // 释放监视点
    else
        printf("unexpected number, delete failed\n");  // 没有找到监视点
}


void info_wp(){
    WP *p = head;  // 从头开始遍历监视点链表
    while (p != NULL) {
        printf("Watchpoint %d: %s = %d\n", p->NO, p->args, p->val);  // 打印监视点信息
        p = p->next;  // 移动到下一个监视点
    }
}

```



添加头文件`/home/camelu1/NEMU2021/nemu/include/monitor/watchpoint.h`

```c
typedef struct watchpoint {
	int NO;
	struct watchpoint *next;
	int val;
    char args[32];
	char exp[32];
	uint32_t value;

	/* TODO: Add more members if necessary */
} WP;

WP* new_wp();
int free_wp(WP*);
void delete_wp(int);
void info_wp();
bool check_wp();
int test_change(); 
```



## PA2 指令系统

参考博客：

https://www.cnblogs.com/grapefruit-cat/p/17153408.html

[NEMU PA2实验思路-CSDN博客](https://blog.csdn.net/weixin_43877657/article/details/120000334?ops_request_misc=%7B%22request%5Fid%22%3A%227ED1E446-1F87-456F-82A1-EF0308197D3B%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=7ED1E446-1F87-456F-82A1-EF0308197D3B&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-120000334-null-null.142^v100^pc_search_result_base9&utm_term=pa2思路分享&spm=1018.2226.3001.4187)

实验手册：

[PA2-指令系统.pdf](file:///C:/Users/10648/AppData/Local/Temp/daaafff0-71db-4ec6-819b-12f1ca461cf0_实验指导书.zip.cf0/实验指导书/PA2-指令系统.pdf)

##### 思考题 1：main 函数返回到哪里 查看 testcase 的相关代码,你知道用户程序从 main 函数返回之后会跳转到哪 里吗？如果用户程序在 GNU/Linux 中运行, 问题的答案又是什么？

返回后，程序会跳转到操作系统的运行时环境，通常是操作系统的 C 运行时库中的 `exit` 函数。这会处理清理工作，然后最终返回控制权给操作系统。

在 GNU/Linux 中，当 `main` 函数返回时，返回值会被传递给 `exit` 系统调用。

### 阶段一

#### 必做任务 1：运行用户程序 mov-c

修改工程目录下的 Makefile 文件, 更换 NEMU 的用户程序：

```c
56| --- USERPROG := obj/testcase/mov
56| +++ USERPROG := obj/testcase/mov-c 
```

修改后, 在终端键入

`make run`

使用新的用户程序运行 NEMU, 你会发现 NEMU 输出以下信息：

![image-20240909192313304](C:\Users\10648\AppData\Roaming\Typora\typora-user-images\image-20240909192313304.png)

添加指令:`/home/camelu1/NEMU2021/nemu/src/cpu/exec/arith`

查i386手册第十七章，找到对应的指令名的对应的opcode，将其形式以：`instr_XXX_X`填入`exec.c`的表中（具体格式见PA2实验指导书,`instr`为指令名称）

- 创建`instr.h`文件 文件内容模仿已有的其他的文件即可

- 创建`instr.c`文件，将所有`_v`后缀的形式填入`make_helper_v(...)`中，其他形式模仿已有文件；

- 创建`instr-template.h`文件，若该指令译码方式存在（具体形式看`decode`相关文件），只需要填入`make_instr_helper`中，再实现`do_execute`完成实现函数即可；若译码方式不存在，自己写`make_helper`函数（模仿`mov-template.h`）实现译码+实现功能，最后return eip的偏移量

在`all-instr.h`里引用文件

```

call将要读取的下一条指令首地址压栈，设置跳转地址；

sub就是在sbb的基础上删去获取cf位和减去cf位的两行代码；

xor就是异或操作之后再根据i386手册写的更新标志位；

leave 将esp ebp恢复为最近一次enter之前的值;

cltd:将eax或ax的最左边一位赋给edx或dx的每一位。读取eax的值，算术右移;

add:相加。更新zf,sf。判断两个加数与和的大小，若两个加数都大于和，说明有进位或者借位，cf=1。判断两个加数的最高位是否相同，若不相同则不会溢出，若加数的最高位相同，判断加数与和的最高位是否相同，若不相同则不会溢出，否则溢出，of=1;

inc: dest<-dest+1,类似add;

sub:根据sbb来写;

dec:dest<-dest-1,类似sub;

cmp:相当于sub，只是不改变操作数，只修改eflags;

neg:如果dest为0，则cf=0,否则为1；将dest取反加一,也就相当于0-dest;

adc的eflags：同add的eflags;

剩余的：用rtl实现，然后按照i386手册所说修改eflags；

setcc：在cc.c中，根据i386中每条跳转指令对应的条件eflags填写；

make_Helper函数要在all-instr.h中声明。
```

#### 必做任务 2：实现更多指令

注意事项：

一些指令需要更新`elfags`，需要自己添加，主要是逻辑运算指令和算术运算指令，找下面这个注释来添加：

`/home/camelu1/NEMU2021/nemu/src/cpu/exec/arith/adc-template.h`

`/home/camelu1/NEMU2021/nemu/src/cpu/exec/arith/sbb-template.h`

```c
/* TODO: Update EFLAGS.*/
```

##### 思考题 2：比较 FLOAT 和 float FLOAT 和 float 类型的数据都是 32 位, 它们都可以表示 2^32 个不同的数, 但由 于表示方法不一样, FLOAT 和 float 能表示的数集是不一样的。思考一下, 我们 用 FLOAT 来模拟表示 float , 这其中隐含着哪些取舍?

`float` 类型在表示小数时具有更高的精度，特别是在处理非常小或非常大的数时。`FLOAT` 的表示方法可能导致精度损失，尤其是在进行浮点运算时。

`float` 的舍入方式通常是根据 IEEE 754 标准进行的，这样可以保证运算的一致性和可预测性。使用 `FLOAT` 可能会导致不同的舍入策略，从而影响计算结果的准确性。

#### 必做任务 3：实现 binary scaling

修改函数`/home/camelu1/NEMU2021/lib-common/FLOAT.h`：

`F2int`函数需要截取定点数前几位：

```c
static inline int F2int(FLOAT a) {
	int ret = a & 0xffff0000;
	return ret >> 16;
}
```

`int2F`需要把整数部分放到高16位：

```c
static inline FLOAT int2F(int a) {
	return a << 16;
}
```

修改函数`/home/camelu1/NEMU2021/lib-common/FLOAT/FLOAT.c`:

`f2F`函数:

```c
FLOAT f2F(float a) {
	/* You should figure out how to convert `a' into FLOAT without
	 * introducing x87 floating point instructions. Else you can
	 * not run this code in NEMU before implementing x87 floating
	 * point instructions, which is contrary to our expectation.
	 *
	 * Hint: The bit representation of `a' is already on the
	 * stack. How do you retrieve it to another variable without
	 * performing arithmetic operations on it directly?
	 */

	Float f;
	void *temp = &a;
	f.val = *(uint32_t *)temp;
	uint32_t m = f.m | (1 << 23);
	int shift = 134 - (int)f.e;
	if(shift < 0) m <<= (-shift);
	else m >>= shift;
	return (_sign(f.val) ? -m : m);
}
```

`lib-common/FLOAT/Makefile.part `，直接替换成下面即可：

```c
# This file will be included by the Makefile under the project directory.

FLOAT_O := $(FLOAT:.a=.o)
FLOAT_VFPRINTF_O := $(dir $(FLOAT))FLOAT_vfprintf.o

FLOAT_A_OBJ := $(FLOAT_O) $(FLOAT_VFPRINTF_O)

$(FLOAT): $(FLOAT_A_OBJ)
	ar r $@ $^

# TODO: complete the following rules

FLOAT_CFLAGS := -O2 -m32 -fno-builtin -fno-stack-protector -D_FORTIFY_SOURCE=0 -march=i386 -mtune=i386

$(FLOAT_O):
	mkdir -p obj/lib-common/FLOAT
	$(CC) $(FLOAT_CFLAGS) -c lib-common/FLOAT/FLOAT.c -o $(FLOAT_O) -Ilib-common

$(FLOAT_VFPRINTF_O):
	mkdir -p obj/lib-common/FLOAT
	$(CC) $(FLOAT_CFLAGS) -c lib-common/FLOAT/FLOAT_vfprintf.c -o $(FLOAT_VFPRINTF_O) -Ilib-common

```

#### q1：报错 error: bits/libc-header-start.h: No such file or directory

缺少 `bits/libc-header-start.h` 文件问题，

**解决方案：**

1. **确保 32 位的 libc 库已安装**：

   你需要安装 32 位版本的 C 库开发头文件。可以通过以下命令安装：

   ```bash
   sudo apt-get update
   sudo apt-get install libc6-dev-i386
   ```

2. **检查系统头文件是否完整**：

   安装缺少的 `glibc` 开发包：

   ```bash
   sudo apt-get install libc6-dev
   ```

3. **如果你不需要 32 位编译**，可以考虑去掉 `-m32` 选项，这样系统会默认使用 64 位环境下的头文件和库。

#### q2：报错 error: "_FORTIFY_SOURCE" redefined [-Werror]

此处编译错误是由于ubuntu与GCC版本不匹配导致的

解决方法：

修改源码目录下`/home/camelu1/NEMU2021/lib-common/FLOAT/Makefile.part`文件：

将以下语句

```c
-D_FORTIFY_SOURCE=0
```

修改为

```c
-U_FORTIFY_SOURCE -D_FORTIFY_SOURCE=0
```

#### q3：安装readelf

```dash
sudo apt-get install binutils
```



##### 思考题 3：消失的符号 我们在 add.c 中定义了宏 NR_DATA, 同时也在 add()函数中定义了局部变量 c 和形参 a, b, 但你会发现在符号表中找不到和它们对应的表项, 为什么会这 样？思考一下, 什么才算是一个符号(symbol)

符号通常指的是在程序中定义的名称，用于表示变量、函数、类型、宏等

在 `add.c` 中，`c`、`a` 和 `b` 是局部符号，它们的作用域仅限于 `add()` 函数，因此可能不会在符号表中找到它们的表项。相反，宏 `NR_DATA` 是在预处理阶段处理的，不会在符号表中记录。符号表主要记录全局符号和具有持久作用域的符号。

#### 必做任务 4：为表达式求值添加变量的支持

要得到某个程序中的某个字符串的值（如`*test_data`，表示该数组第一个值）。所以我们需要现在`expr.c`中添加对这种字符串的正则分解的支持：

```c
{"\\b[a-zA-Z0-9_]+\\b",MARK}
```

然后通过上面的`elf`文件来查询，字符串表在`elf`文件的`.strtab`段中，其中从该地址（`off`）往后偏移`size`长度均为该测试用例的全局变量的值，包括`add.c`、`main`、`test_data`等等，这也都是用ascii码来存储的，顺序为`.symtab`从上到下的顺序（`.symtab`的`Name`表示该串从`off`地址第几个开始）

我们要识别例如`test_data`而不是`main`，需要判断`.symtab`的类型是否为`OBJECT`

##### 思考题 4：堆和栈在哪里? 我们提到了代码和数据都在可执行文件里面, 但却没有提到堆(heap)和栈 (stack)。为什么堆和栈的内容没有放入可执行文件里面？那程序运行时刻用到 的堆和栈又是怎么来的？

堆和栈的内容在程序运行时动态生成，并且其大小和状态依赖于程序的执行过程，因此它们不会被包含在可执行文件中。操作系统负责在程序启动时为堆和栈分配内存。

##### 思考题 5：如何识别不同格式的可执行文件？ 如果你在 GNU/Linux 下执行一个从 Windows 拷过来的可执行文件, 将会报告" 格式错误"。思考一下, GNU/Linux 是如何知道"格式错误"的？

GNU/Linux 系统通过检查可执行文件的魔数来识别文件格式。如果魔数不符合已知格式，内核会报告“格式错误”。这种机制确保了系统只能执行有效的可执行文件格式，从而避免了潜在的错误和安全风险。

##### 思考题 6：冗余的属性？ 使用 readelf 查看一个 ELF 文件的信息, 你会看到一个 segment 包含两个大小 的属性, 分别是 FileSiz 和 MemSiz, 这是为什么? 再仔细观察一下, 你会发现 FileSiz 通常不会大于相应的 MemSiz, 这又是为什么?

`FileSiz` 和 `MemSiz` 的存在是为了区分文件的存储结构和内存的使用结构。`FileSiz` 通常小于或等于 `MemSiz`，主要是由于内存对齐和填充的需要。这种设计确保了程序在运行时能够有效地使用内存，同时保持文件的紧凑性。

## PA3 存储管理

参考博客：

[NEMU PA 3-1 实验报告 - GrapefruitCat - 博客园 (cnblogs.com)](https://www.cnblogs.com/grapefruit-cat/p/17154132.html)

