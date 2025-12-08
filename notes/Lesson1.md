Unix系统中成功的返回码是 0 ，遇到问题返回码为 1


代码片段*
char *argv[] = { "echo", "THIS", "IS", "ECHO", 0 };
exec("echo", argv);
解析：
1. char *argv[] = { ... }
定义： 这一行定义了一个名为 argv 的 字符串指针数组 (Array of String Pointers)。
作用： 这个数组就是新程序（这里是 "echo"）将接收到的命令行参数列表。
结构：
"echo"： 数组的第一个元素 (argv[0]) 必须是程序本身的名称。这是 Unix 约定。
"THIS", "IS", "ECHO"： 实际传递给程序的参数。
0 (NULL)： 数组必须以一个空指针 (0 或 NULL) 结束，这是程序在解析参数时判断列表结束的标志。

2. exec("echo", argv);
调用： 这是对 exec 系统调用的调用。
作用： exec 会尝试用指定的新程序替换当前正在执行的程序。
第一个参数 ("echo")： 指定要加载和执行的可执行文件路径（在 xv6 中，内核会在 / 和 /bin 目录中查找该程序）。
第二个参数 (argv)： 传递给新程序的命令行参数数组。
执行结果：
成功： 如果 exec 成功找到并加载了 "echo" 程序，当前进程的代码和数据将被销毁，并被 "echo" 程序替换。程序计数器 (PC) 会跳转到 "echo" 的入口点，它开始执行。
失败： 如果 exec 失败（例如，找不到 "echo" 文件，或文件格式错误），它将返回一个错误值给调用者。

fork先复制父进程创建一个子进程，然后exec再把子进程清空替换成我们想换的程序

重定向
A. 输入重定向 符号为<  格式：command < file 含义command程序不再等待键盘输入而是直接从指定的file文件读取内容
B. 输出重定向 (> 和 >>) 一个覆盖一个追加
格式：command > file将 command 的标准输出（FD 1）从屏幕改为写入 file。如果 file 存在，会覆盖其原有内容。ls > files.txt：将 ls 的输出写入 files.txt，覆盖旧内容。
格式：command >> file将 command 的标准输出（FD 1）改为写入 file。如果 file 存在，会在文件末尾追加新内容。date >> log.txt：将当前日期追加到 log.txt 的末尾。

重定向的实现机制
在 Shell 执行命令时，重定向的实现依赖于 fork、exec 和 close/open/dup 这三个系统调用的组合：

步骤 1: 复制 (Fork)
Shell 调用 fork() 创建一个子进程。
步骤 2: 修改文件描述符 (Close/Open/Dup)
在子进程中，但在调用 exec 之前，Shell 会检查是否存在重定向符号 (< 或 >)。
如果存在重定向（例如 echo hello > output.txt）：
子进程首先调用 close(1)（关闭标准输出，使其文件描述符 1 处于空闲状态）。
接着调用 open("output.txt", O_CREATE | O_WRONLY)。由于文件描述符表是按最小可用原则分配的，这个新的文件描述符就会被分配到 1。
结果： 此时，子进程的标准输出（FD 1）不再指向屏幕，而是指向了 output.txt 文件。
步骤 3: 替换 (Exec)
子进程调用 exec("echo", ...)。
exec 替换了代码，但保留了文件描述符表。因此，当新的 echo 程序运行时，它向文件描述符 1 写入的任何数据，都会自动写入 output.txt 文件，而不是屏幕。









