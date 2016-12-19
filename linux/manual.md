+ 查看进程(按CPU倒序)
	
	```
	$ ps -e -o "%C : %p : %z : %a"|sort -nr
	```
+ 查看进程(按内存倒序)

	```
	$ps -e -o "%C : %p : %z : %a"|sort -k5 -nr
	```
+ 查看剩余内存(单位MB)

	```
	$free -m |grep "Mem" | awk '{print $2}'
	```
+ 查看磁盘占用情况

	```
	$df -h
	```
+ 查看当前目录文件大小

	```
	$du -h
	```