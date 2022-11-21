#### 一、Bash与Shell

##### 1. shell

- 能够操作应用程序的接口的壳程序；
- /bin/bash 是 linux 默认的 shell；

##### 2. Bash Shell

- 命令编修能力：~/.bash_history 记录前一次登陆以前所执行过的指令， 至于这一次登陆所执行的指令都被暂存在内存中，当你成功的登出系统后，该指令记忆才会记录到 .bash_history 当中；

- 命令与文件补全功能：[Tab]按键；

- 命令别名设置功能

  ```bash
  alias # 显示所有命令别名
  alias lm=‘ls -al’ # 设置命令别名
  ```

- 工作控制、前景背景控制；

- 程序化脚本：shell script；

- 万用字符；

##### 3. 查询是否为Bash shell内置命令

```bash
type [-tpa] name
```

```
不加任何选项与参数时，type 会显示出 name 是外部指令还是 bash 内置指令
-t：当加入-t参数时，type 会将 name 以下面这些字眼显示出他的意义：
      file：表示为外部指令；
      alias：表示该指令为命令别名所设置的名称；
      builtin：表示该指令为 bash 内置的指令功能；
-p：如果后面接的 name 为外部指令时，才会显示完整文件名；
-a：会由 PATH 变量定义的路径中，将所有含 name 的指令都列出来，包含 alias；
```

##### 4. 指令的下达与快速编辑按钮

- 使用 \ + [Enter] 可以跳行
- [ctrl] + u 从光标处向前删除指令串， [ctrl] + k 向后删除指令串。
- [ctrl] + a 让光标移动到整个指令串的最前面，[ctrl] + e 移动到最后面。

#### 二、Shell的变量功能

##### 1. 变量的取用、删除、设置

- 变量的取用

  ```bash
  echo $变量名 或 ${变量名}
  ```

- 变量的删除

  ```bash
  unset $变量名
  ```

- 变量的设置

  ```bash
  变量名=变量内容 # 设置一个变量
  ```

  - 等号两边不能直接接空白字符；
  - 变量名称只能是英文字母与数字，开头字符不能是数字；
  - 变量内容有空白字符可以使用单引号与双引号，双引号内的特殊字符保持原有特性，单引号内的特殊字符仅为一个字符；
  - 可以使用跳脱字符 \ 将特殊符号（[Enter]、$、\，空白字符等）变成一般字符；
  - 使用反单引号``或者$(指令)可以在一串指令中执行另一条指令；
  - 若该变量为扩增变量内容时，则可用 "$变量名称" 或 ${变量} 累加内容；
  - 若该变量需要在其他子程序执行，则需要以 export 来使变量变成环境变量；
  - 通常大写字符为系统默认变量，自行设置的变量使用小写字符；

##### 2. 环境变量

- 环境变量的内容

  - HOME：代表使用者的主文件夹；
  - SHELL：环境使用的SHELL是哪支程序；
  - HISTSIZE：记录历史命令的数量；
  - MALL：系统去读取邮件信箱文件；
  - PATH：可执行文件的搜寻路径；
  - LANG：语系数据；
  - RANDOM：产生一个随机数（0～32768）；

- 观察所有变量：set

  - PS1：提示字符的设置；
  - $：目前这个SHELL的线程代号（PID）；
  - ?：关于上个执行指令的回传值，成功执行回传0；
  - OSTYPE、HOSTTYPE、MACHTYPE：主机硬件与核心的等级；

- 自定变量转环境变量：export

  ```bash
  export 变量名称 #没有接环境变量就显示所有的环境变量
  ```

- 语系变量

  ```bash
  locale -a #显示支持的所有语系
  ```

  - 设置LANG和LC_ALL时，其他语系变量就会被这两个取代；
  - /etc/locale.conf中存放系统默认语系；

- 变量的有效范围：环境变量可以被子程序所引用，自定变量不会存在子程序中；

##### 3. 变量键盘读取、阵列与宣告

- read：读取来自键盘输入的变量；

  ```bash
  read [-pt] variable
  ```

  ```bash
  -p：后面可以接提示字符;
  -t：后面可以接等待的秒数;
  ```

- declare/typeset：宣告变量类型；

  ```bash
  declare [-aixr] variable #不接任何参数显示所有变量
  ```

  ```bash
  -a：将后面名为 variable 的变量定义成为阵列 （array） 类型；
  -i：将后面名为 variable 的变量定义成为整数数字 （integer） 类型；
  -x：用法与 export 一样，就是将后面的 variable 变成环境变量；
  -r：将变量设置成为 readonly 类型，该变量不可被更改内容，也不能 unset;
  -p：单独列出变量类型；
  ```

  - 变量类型默认为字串；
  - bash环境中的数值运算默认最多仅能达到整数形态；

- 阵列变量类型

  ```bash
  a[1]="one" 
  a[2]="two" #设置
  echo $a #读取 one two
  ```

##### 4. 与文件系统及程序

```bash
ulimit [-SHacdfltu] [配额]
```

```bash
-H：hard limit ，严格的设置，必定不能超过这个设置的数值；
-S：soft limit ，警告的设置，可以超过这个设置值，但是若超过则有警告讯息。在设置上，通常 soft 会比 hard 小；
-a：后面不接任何选项与参数，可列出所有的限制额度；
-c：当某些程序发生错误时，系统可能会将该程序在内存中的信息写成文件（除错用），这种文件就被称为核心文件（core file）。此为限制每个核心文件的最大容量；
-f：此 shell 可以创建的最大文件大小（一般可能设置为 2GB）单位为 KBytes；
-d：程序可使用的最大断裂内存（segment）容量；
-l：可用于锁定 （lock） 的内存量；
-t：可使用的最大 CPU 时间 （单位为秒）；
-u：单一使用者可以使用的最大程序（process）数量；
```

##### 5. 变量内容的删除、取代与替换

- 变量内容的删除

  ```bash
  ${变量#关键字} #若变量内容从头开始的数据符合“关键字”，则将符合的最短数据删除
  ${变量##关键字} #若变量内容从头开始的数据符合“关键字”，则将符合的最长数据删除
  ```
  
  ```bash
  ${变量%关键字} #若变量内容从尾向前的数据符合“关键字”，则将符合的最短数据删除
  ${变量%%关键字} #若变量内容从尾向前的数据符合“关键字”，则将符合的最长数据删除
  ```
  
- 变量内容的取代

  ```bash
  ${变量/旧字串/新字串} #若变量内容符合“旧字串”则“第一个旧字串会被新字串取代”
  ${变量//旧字串/新字串}	#若变量内容符合“旧字串”则“全部的旧字串会被新字串取代”
  ```

- 变量的测试

  | 变量设置方式     | str 没有设置       | str 为空字串       | str 已设置非为空字串 |
  | ---------------- | ------------------ | ------------------ | -------------------- |
  | var=${str-expr}  | var=expr           | var=               | var=$str             |
  | var=${str:-expr} | var=expr           | var=expr           | var=$str             |
  | var=${str+expr}  | var=               | var=expr           | var=expr             |
  | var=${str:+expr} | var=               | var=               | var=expr             |
  | var=${str=expr}  | str=expr var=expr  | str 不变 var=      | str 不变 var=$str    |
  | var=${str:=expr} | str=expr var=expr  | str=expr var=expr  | str 不变 var=$str    |
  | var=${str?expr}  | expr 输出至 stderr | var=               | var=$str             |
  | var=${str:?expr} | expr 输出至 stderr | expr 输出至 stderr | var=$str             |


#### 三、命令别名与历史命令

##### 1. 命令别名设置

- 查看命令别名

  ```bash
  alias
  ```

- 设置命令别名

  ```bash
  alias 别名=指令
  ```

- 取消命令别名

  ```bash
  unalias 别名
  ```

##### 2. 历史命令

```bash
history [n]
history [-c]
history [-raw] histfiles
```

```bash
n ：数字，意思是“要列出最近的 n 笔命令列表”的意思；
-c：将目前的 shell 中的所有 history 内容全部消除；
-a：将目前新增的 history 指令新增入 histfiles 中，若没有加 histfiles ，则默认写入 ~/.bash_history；
-r：将 histfiles 的内容读到目前这个 shell 的 history 记忆中；
-w：将目前的 history 记忆内容写入 histfiles 中；
```

```bash
!number #执行第几笔指令的意思
!command #由最近的指令向前搜寻“指令串开头为 command”的那个指令，并执行
!! #执行上一个指令
```

#### 四、Bash Shell的操作环境

##### 1. 路径与指令搜寻顺序

- 以相对/绝对路径执行指令，例如“ /bin/ls ”或“ ./ls ”；
- 由 alias 找到该指令来执行；
- 由 bash 内置的 （builtin） 指令来执行；
- 通过 $PATH 这个变量的顺序搜寻到的第一个指令来执行。

##### 2. bash的进站与欢迎讯息

- 本地登录：/etc/issue；
- 远端登录：/etc/issue.net；
- 提示信息：/etc/motd；

##### 3. bash的环境配置文件

- 

