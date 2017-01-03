##编写自己的service

最近在玩Liunx，发现linux启动服务是用SERVICE + COMMAND，觉得很有意思，因为command命令本身也是一个脚本啊，比如说：service network restart；好奇心就来了，怎么能够做一个属于自己的service命令呢。

其实很简单，只要我们认识service这个命令的原理就行了。如果要知道service这个命令怎么用，你就自己man service下，在这里，我简要说下service的运行过程。举个例子来说：service network restart。

首先呢，sevice 会去寻找/etc/init.d下的network脚本，restart是network脚本里的一个参数（你可以去查看network这个脚本支持的参数），然后告诉系统运行network这个脚本，剩下的事情就交给network脚本去坐了，事实就是这么简单。

现在，你应该知道怎么编写属于自己的service命令了吧，编写一个脚本，然后把它放在/etc/init.d这个目录底下，你就可以用service +脚本名字 运行它。如果是要开机自动启动那就得用chkconfig命令了。

注意：

A、service这个命令往往是即时生效，不用开关机，但是重启后服务会回到默认状态。

B、chkconfig是用于把服务加到开机自动启动列表里，只要启动它，就能自动启动，重启后永久生效

即：chkconfig --add COMMAND 

chkconfig COMMAND on/off    重启后永久生效
