
## 引号
- ""

不完全引用，内部有命令会执行
- ''

完全引用，内部有命令不会执行，原样输出
- ``

执行内部的命令，相当于$()

## 括号

- ()

常见一个子shell执行/初始化一个数组
- (())

进行整数运算或者定义变量
- []

相当于test，用于判断，内部不能有<>,||和&&等比较运算符，只能用=或者!=(只能用作字符串比较)，可用 -gt,-eq,-lt,-ge,-le等代替
- [[]]

shell中的关键字，扩展了[]
- {}

可表示范围，如{1..3}，或通配文件名，如{a,b}cd 代表acd和bcd

## 命令行参数

- $0 脚本名称
- $* 输入参数
- $@ 输入参数
- $# 输入参数个数
- $? 上条命令执行结果
- $$ 子进程运行的pid

## 变量

### 变量替换
- ${变量#匹配规则}

从头开始匹配。最短删除
```
variable="I love you, do you love me?"

variable1=${variable#*ov}

$ echo $variable1
e you, do you love me?
```

- ${变量##匹配规则}

从头开始匹配。最长删除

```
variable2=${variable##*ov}

$ echo $variable2
e me?
```

- ${变量%匹配规则}

从尾开始匹配，最短匹配
```
variable3=${variable%ov*}

$ echo $variable3
I love you, do you l
```
- ${变量%%匹配规则}

从尾开始匹配，最长匹配

- ${变量/旧字符串/新字符串}

替换变量内旧字符串为新字符串，只替换**第一个**匹配的字符串

- ${变量//旧字符串/新字符串}

替换变量内旧字符串为新字符串，全部替换

## 运算

- expr

只能用做整数运算

```
$ echo `expr 1 + 1`
2
```

- bc

可用作整数，浮点数，可指定scale

```
$ echo "scale=2;13/2" | bc
6.50
```

## 字符串处理

- 计算字符串长度

len=${#val}

len=`expr lenth "${val}"`

- 获取字符串索引位置

expr index "${val}" subVal

其实是将subVal分成字符，找出第一个匹配字符的位置

- 获取子串长度

expr match "${val}" subVal

子串必须从头开始匹配

- 提取子串

${val:index}：从index开始截取字符串到变量末尾(下标从0开始)
${val:index:length}从index开始提取长度为length的字符串
${val: -index:length}从尾部，index开始提取子串(或${val:(-index)})

### expr计数
下标从1开始计数

## 变量声明

### declare

- -r 声明变量为只读变量
- -i 声明变量为整形
- -f 查看系统函数和内容
- -F 查看系统函数名
- -a 声明数组

```
array=(1 2 3 4 5)
echo ${array}
echo ${array[@]}
echo ${array[*]}
```
- -x 声明为环境变量
