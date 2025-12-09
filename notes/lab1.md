### sleep函数实现思路
# A.处理命令行参数
xv6内核中的sleep()系统调用接受的参数是ticks不是秒
用户输入sleep 5时，程序需要：
1、获取参数：通过main函数的参数argc和acgv获取命令行输入
2、确保用户提供有且只有一个参数，即argc必须等于2，如果数量错误，程序应打印错误信息并退出
3、字符串转整数： 使用 xv6 提供的库函数 atoi() (ASCII to Integer) 将命令行参数（字符串）转换为整数。
# B.调用系统调用并退出
1.将秒数转换为 ticks：ticks = seconds * TICKS
2.调用内核函数 sleep(ticks)
3.调用exit()安全终止进程

//argc 的值总是等于 argv 数组中有效字符串的个数，而argv数组的第“0”个值总是程序名，这就使为什么要求argc等于2，一个是程序名本身另一个是睡眠时间

qemu模拟器退出指令：ctrl+a 松开后按x














