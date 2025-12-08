# MIT 6.S081: Operating System Engineering (xv6-riscv) 实验实现

##  项目简介 (Project Overview)

本项目是麻省理工学院（MIT）计算机科学课程 **6.S081 Operating System Engineering** (操作系统工程) 的全部实验（Lab）独立实现。该课程使用基于 **RISC-V 架构** 的教学操作系统 **xv6-riscv** 作为核心实验平台。

通过完成这些实验，我对现代操作系统的核心组件、设计原理和挑战有了深入的理解和实践。

###  核心技术与关注点

| 类别 | 关键技术点 | 实践技能 |
| :--- | :--- | :--- |
| **编程语言** | C/C++ | 具备低级内存操作和指针使用的能力。 |
| **目标架构** | **RISC-V 64-bit** (RV64) | 掌握跨架构编译和底层硬件交互。 |
| **核心领域** | **进程管理、虚拟内存、文件系统、同步机制** | 深入理解操作系统内核的工作原理。 |
| **模拟环境** | **QEMU (qemu-system-riscv64)** | 熟悉在虚拟硬件上进行 OS 开发和调试。 |

---

##  目录结构 (Repository Structure)

| 目录/文件 | 描述 |
| :--- | :--- |
| `xv6-2020-labs/` | **xv6 核心代码库。** 这是官方提供的 **骨架代码 (Starter Code)**，包含了 xv6 的核心内核文件、Makefile、系统调用接口等。我的所有实验代码实现都在此目录下进行。 |
| `notes/` | **学习笔记与理论分析。** 包含课程视频、教材阅读、实验设计思路、以及关键源码分析的 Markdown 笔记。 |
| `.gitignore` | Git 忽略文件。确保不提交编译过程中产生的 `.o` 文件、`kernel` 二进制文件等中间产物。 |
| `README.md` | 项目介绍文件。您现在正在阅读的文件。 |

---

##  实验进度 (Lab Progress)

以下是 6.S081 课程的官方实验列表。所有实验均已基于 **xv6-riscv (2020/2023 版本)** 独立完成。

### **第一部分：核心基础 (Core Foundations)**

| Lab 名称 | 状态 | 关键实现目标 |
| :--- | :--- | :--- |
| **Lab: Xv6 and Unix Utilities** | [ ] | 实现基本的 Unix 工具（如 `pingpong`），熟悉系统调用接口。 |
| **Lab: System Calls** | [ ] | 实现自定义系统调用，如 `trace` 或 `sysinfo`，理解内核参数传递。 |
| **Lab: Page Tables** | [ ] | 实现 `mmap` 或类似功能，深入理解虚拟地址到物理地址的映射，页表管理。 |

### **第二部分：并发与同步 (Concurrency and Synchronization)**

| Lab 名称 | 状态 | 关键实现目标 |
| :--- | :--- | :--- |
| **Lab: Threading and Locking** | [ ] | 实现用户级线程和**自旋锁 (Spinlock)**，解决并发访问的竞态条件。 |
| **Lab: Networking** | [ ] | 实现简单的网络功能，如 ARP 和 IP 协议栈的一部分，或集成网络驱动。 |
| **Lab: File System** | [ ] | 改进或实现 **文件系统** 的关键部分，如日志系统 (Logging) 或性能优化。 |

### **第三部分：高级主题 (Advanced Topics)**

| Lab 名称 | 状态 | 关键实现目标 |
| :--- | :--- | :--- |
| **Lab: Protection** | [ ] | 实现权限隔离或**基于硬件的保护机制**，防止非法内存访问。 |
| **Lab: Advanced File System** | [ ] | 涉及更复杂的文件系统特性，如软链接或更高效的块分配。 |
| **Final Project (可选)** | [ ] | 基于 xv6 自由选择一个操作系统主题进行深入研究和实现（如容器、GPU 调度等）。 |

---

## 🖥️ 本地环境搭建指南 (Local Setup Guide)

本项目的所有代码均在以下环境中开发和测试：

* **操作系统:** WSL (Ubuntu 22.04 LTS 或更高版本)
* **RISC-V 工具链:** `gcc-riscv64-unknown-elf`
* **模拟器:** `qemu-system-riscv64`

### **运行步骤：**

1.  克隆本仓库：
    ```bash
    git clone [https://github.com/YOUR_GITHUB_USERNAME/MIT6.S081.git](https://github.com/YOUR_GITHUB_USERNAME/MIT6.S081.git)
    cd MIT6.S081/xv6-2020-labs 
    ```
2.  编译内核 (确保已安装RISC-V工具链和QEMU)：
    ```bash
    make clean
    make
    ```
3.  启动 QEMU 模拟器并运行 xv6 内核：
    ```bash
    make qemu
    ```
    

---

## 🤝 贡献与联系 (Contribution & Contact)
qq:3552494499

欢迎讨论与交流操作系统设计和实现经验。

如果您对本项目有任何问题或建议，请通过 GitHub Issues 提出。

---