### PHP程序员应该具备的调试能力
---
	    个人认为解决问题的能力是排第一位的，比学习能力优先级更高。解决问题的能力既能看出程序员的思维能力，应变能力，探索能力等，
	又可以看出他的经验。本篇主要介绍8种调试方法。
---

#### Lv0: 存在多个版本的php或php-cli与php-fpm加载不同的配置
	    存在多个版本的php，懂得通过which php来看是哪个PHP，或者加绝对路径制定php版本。表示此PHPer通过了此层级的50%考验。
	    
	    另外一个情况就是php-cli与php-fpm得到的执行情况不一样，如在web浏览器中执行是对的，cli下执行是错的。这时候可能是2个环境
	加载的php.ini不同所致。cli下通过php -i |grep php.ini得到加载了哪个php.ini。而fpm下通过phpinfo()函数可以得到php.ini
	的绝对路径。

#### Lv1: var_dump/die打印变量值信息单步调试
	    这是惯用的程序调试手段，也是最简单粗暴有效的解决问题方法。高级一点的手段是使用PHP的Trace类/日志类，花哨一点的可以借助
	phpstorm+xdebug在IDE工具里进行Debug。
		
	    Trace工具还可以分析脚本的耗时，进行PHP程序的性能优化。
#### Lv2: 查看PHP错误信息
	    程序没有达到预期效果，证明代码出错了，看PHP的错误信息是第一步。如果直接忽略错误信息，表明这个人不适合担任专业的程序员
	岗位。有些情况下php.ini配置中关闭了错误显示，需要修改php.ini打开错误信息，或者错误信息被导出到了日志文件，这种情况可以直
	接tail -f php_error.log来看错误信息。拿到错误信息后直接定位到程序代码问题，或者到Google/百度搜索，即可解决问题。

	注：打开错误显示的方法是
		 php.ini中display_errors / display_startup_errors 设置为On
		 php.ini中error_reporting 设置为E_ALL
		 PHP代码中设置error_reporting(E_ALL)
#### Lv3: 分析函数调用的耗时和成功率
	    使用xhporf/xdebug导出PHP请求的调用过程，然后分析每个函数调用的过程和耗时。能够分析PHP程序的性能瓶颈，找出可以优化
	的点。

	    另外一个对于网络服务的调用，如mysql查询，curl，其他API调用等，通过记录起始和结束时microtime，返回的是不是false，
	可以得到调用是否成功，耗时多少。如果可以汇总数据，整理出调用的成功率，失败率，平均延时，证明此程序员对接口质量敏感，有大型
	网站项目经验。
#### Lv4: 使用tcpdump工具分析网络通信过程
	    tcpdump可以抓到网卡的数据通信过程，甚至数据内容也可以抓到。使用tcpdump可以看到网络通信过程是什么样的，如何时发起了
	TCP SYN3次握手，何时发送FIN包，何时发送RST包。这是一个基本功，如果不懂tcpdump，证明不具备网络问题解决能力。
#### Lv5: 使用strace工具跟踪程序执行
	    strace可以用来查看系统调用的执行，使用strace php test.php，或者strace -p 进程ID。strace就可以帮助你透过现象看
	本质，掌握程序执行的过程。这个手段是在大型网站，大公司里最常用的。如果没掌握strace，这里只能说抱歉了，我们不接受不会strace
	的PHPer。

	    strace其实也是对程序员基础的考验，如果不懂操作操作系统，完全不懂底层，肯定也达不到会用strace的程度。当然strace对于
	PHP代码里的死循环是解决不了的。比如你发现一个php-fpm进程CPU100%了，strace恐怕是解决不了的。因为strace是看系统调用，
	一般都是IO类操作，既然是IO密集，那CPU一定不可能是100%。
#### Lv6: gdb使用
	    gdb是C/C++调试程序的利器，需要具备一定C/C++功底的程序员才会能熟练使用gdb。上面说的strace无法跟踪php程序CPU100%，
	    而gdb是可以跟踪的。另外gdb也可以解决php程序core dump的问题。

	    通过gdb -p 进程ID，再配合php-src的.gdbinit zbacktrace等工具，可以很方便地跟踪PHP程序的执行。像上面的CPU100%
	往往是PHP程序中发生死循环了，gdb进行多次查看，就大致可以得到死循环的位置。具备gdb解决问题能力的PHP程序员少之又少。如果
	能使用gdb解决PHP问题，这个PHPer百分之百可以通过面试，并且可以拿到较高的技术评级。
#### Lv7: 查看PHP内核和扩展源码
	    如果能熟悉PHP内核和扩展的源码，遇到PHP程序中最复杂的内存错误，也可以有解决的能力。这类PHP程序员就是凤毛麟角了。配
	合gdb工具和对PHP源码的熟悉，可以查看opcode的信息，execute_data的内存，全局变量的状态等。
