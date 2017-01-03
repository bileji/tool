##Shell $#, $*, $@, $$, $!, $?, $0和命令行参数

###参数列表
>
|变量|含义|
|---|---|
|$#|传递给脚本或函数的参数个数|
|$*|所有参数列表。以"$1 $2 … $n"的形式输出所有参数|
|$@|所有参数列表。以"$1" "$2" … "$n" 的形式输出所有参数|
|$$|当前脚本进程ID|
|$!|脚本中最后运行的后台进程的PID|
|$?|上个命令的退出状态，或函数的返回值|
|$0|当前脚本的名称|

###$*,$@的区别

test.sh脚本

```
#!/bin/bash
echo "\$*=" $*
echo "\"\$*\"=" "$*"
	
echo "\$@=" $@
echo "\"\$@\"=" "$@"
	
echo "print each param from \$*"
for var in $*
do
    echo "$var"
done
	
echo "print each param from \$@"
for var in $@
do
    echo "$var"
done
	
echo "print each param from \"\$*\""
for var in "$*"
do
    echo "$var"
done
	
echo "print each param from \"\$@\""
for var in "$@"
do
    echo "$var"
done
```

执行结果

```
$*=  a b c d
"$*"= a b c d
$@=  a b c d
"$@"= a b c d
print each param from $*
a
b
c
d
print each param from $@
a
b
c
d
print each param from "$*"
a b c d
print each param from "$@"
a
b
c
d
```
