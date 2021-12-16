大概就拿来记一下笔记啥的=0=

---
20211127
# 1. 关系型数据库
1.  六种范式：
    * 第一范式（1NF）：
      * 数据库表的每一列都是不可分割的原子数据项
      * 每一列存储的数据类型要相同
      * 一个table里的所有列都要有unique name
      * 数据存放顺序不重要
    * 第二范式（2NF）：
      * 必须满足1NF
      * no Partial Dependency，非码属性必须完全依赖于候选码
    * 第三范式（3NF）：
      * 必须满足2NF
      * no transitive








# 3. vmware虚拟机练习
[vmware workstation pro 16.0]

### 常用指令
| 指令   | 用途         |
| ------ | ------------ |
| init 3 | 到达字符界面 |
| init 5 | 到达图形界面 |
| init 6 | 重启         |
| init 0 | 关机         |

### 基础概念
* **虚拟机**（Virtual Machine）是计算机系统的仿真器，通过软件模拟具有完整硬件系统功能的、运行在一个完全隔离环境中的完整计算机系统，能提供物理计算机的功能。其本质特点是运行在虚拟机上的软件被局限在虚拟机提供的资源里。
* 虚拟机根据它们的运用和与直接机器的相关性可分为**系统虚拟机**和**程序虚拟机**
  * 系统虚拟机可以提供一个可以运行完整操作系统的完整系统平台，
  * 程序虚拟机则为运行单个计算机程序设计
* 常用的虚拟化技术：
  * 操作系统中内存的虚拟化（将一部分硬盘虚拟化为内存）；
  * 虚拟专用网技术（VPN）在公共网络中虚拟化一条私有网络。
* 两款运行架构：
  * **寄居架构（VMware Workstation）**：适合于学习
  * **原生架构（VMware vSphere）**：一般用于企业生产环境
* 网络类型：
  * **桥接网络**：虚拟机跟主机IP地址不同，虚拟机必须在外部网络有单独的IP地址；
  * **网络地址转换(NAT)**：ip地址相同；
  * **仅主机模式网络**：相当于是个局域网，只能跟本地的主机和其他同网络类型的虚拟机进行通信。
  * <a href="https://docs.vmware.com/cn/VMware-Workstation-Pro/16.0/com.vmware.ws.using.doc/GUID-3B504F2F-7A0B-415F-AE01-62363A95D052.html" target="_blank">为虚拟机选择网络连接类型</a>
* I/O控制器：
  * 是用于实现CPU控制I/O设备的中间件
  * 由指令寄存器InstructionRegister、程序计数器ProgramCounter、操作控制器OperationController组成
  * <a href="http://m.gongkong.com/News/detail?id=405610" target="_blank">I/O控制器简介</a>
* 磁盘类型：
  * IDE：并口；SATA：串口
  * SCSI：小型计算机系统专用接口；SAS：串口的SCSI接口。（一般服务器硬盘用这两类）
  * FC：光纤通道（最初页为网络系统设计）
  * SSD：固态电子硬盘
  * <a href="https://blog.csdn.net/tianlesoftware/article/details/6009110" target="_blank">硬盘类型介绍</a>



> **Q&A**:
> 1. vmware跟virturalBox区别？
> 2. 寄居架构和原生架构的区别？
> 3. VMware版本选择？ -*选个屁无脑选最新*
> 4. Ubuntu还是CentOS？
  *Ubuntu基于Debian架构，CentOS继承自Red Hat Enterprise Linux
  *Ubuntu社区完善，可用的文档较多，出个啥小毛病很容易解决
  *Ubuntu服务器对容器和云部署提供大量支持
  *CentOS可以使用控制面板提供网络托管服务（要部署服务器的话还是先选CentOS吧）
> 5. 处理器数量，每个处理器的内核数量，内核总数（得，硬件系统也得补）
> 6. 给虚拟机分配内存时，多个虚拟系统之间会相互影响吗？
> *暂时不知道，但可以先少分配一点，不够再加（建好可以改），建议低于总内存的一半
> 7. 选择I/O控制器类型：LSI Logic; LSI Logic SAS; 准虚拟化SCSI
> 8. 桥接网络和NAT具体应用环境？


###网络配置
#####主机名管理
| 功能                  | 指令                     |
| --------------------- | ------------------------ |
| 查看主机名            | hostname                 |
| 查看主机名与系统详情  | hostnamectl status       |
| 临时修改主机名        | hostname yzm_localhost   |
| 永久修改-直接修改文件 | vi /etc/hostname         |
| 永久修改-命令行       | hostnamectl set-hostname |
| 重启生效              | init 6                   |
#####网络管理
| 功能 | 指令                        | 备注                                         |
| ---- | --------------------------- | -------------------------------------------- |
| 查看 | ifconfig 或 ifconfig ens160 | 暂时用这个，后面不需要用ifconfig，有其他指令 |
|      |                             |                                              |

---
20211130
### 防火墙
* Selinux: 文件级防火墙
* Firewalld和Iptables：网络级防火墙
  * centOS从5-8用的都是Iptables，从7开始加入Firewalld
*  **Selinux**和**Iptables**
*
| 功能              | 指令                                       | 备注                    |
| ----------------- | ------------------------------------------ | ----------------------- |
| selinux查看       | sestatus                                   |                         |
| selinux关闭       | vi /etc/selinux/config，将SELINUX=disabled |                         |
| firewalld查看     | systemctl status firewalld                 |                         |
| firewalld关闭     | systemctl stop firewalld                   |                         |
| firewalld开机关闭 | systemctl disable firewalld                |                         |
| Iptables查看规则  | iptables -L -n                             |                         |
| Iptables添加规则  | iptables -I INPUT -s 192.168.10.3 -j DROP  | 只是个例子              |
| Iptables清空规则  | iptables -F                                |                         |
| Iptables保存      | service iptables save                      | 详见下方“yum软件包安装” |
|                   |                                            |                         |

* yum软件包安装
  * 挂载光驱：`mount /dev/cdrom /media/`
  * 配置yum：
    * ```
      cd /etc/yum.repos.d
      mv CentOS-Media.repo /mnt/
      rm -rf *
      mv /mnt/CentOS-Linux-Media.repo ./
      vi CentOS-Media.repo
      以下是vi内修改的部分：
      [c8-media-BaseOS]
      baseurl=file:///media/BaseOS
      gpgcheck=0
      enabled=1
      [c8-media-AppStream]
      baseurl=file:///media/AppStream
      gpgcheck=0
      enabled=1
      ```
    * 查看挂载： `df`
    * 查看yum可控制的软件包：`yum list | wc -l`, `yum list | grep iptables`
    * yum安装rpm软件包：`yum -y install iptables-services.x86_64`

### vi编辑器
| 功能       | 指令 |
| ---------- | ---- |
| 保存并退出 | :wq     |


### MySQL数据库练习
<a href="https://zhuanlan.zhihu.com/p/367327903" target="_blank">安装MySQL数据库</a>


###装一下php，建个wordpress站点
```
systemctl stop firewalld.service
yum install php*
service php-fpm start
yum install nginx
service nginx start
```
* "Failed to update metadata..."
  * Edit /etc/yum.repos.d/CentOS-Media.repo and change enabled=1 to 0
* "There are no enabled repositories in "/etc/yum.repos.d"..."
  * 重新挂载光驱（上面有）再```yum install php*```
* ```ps -ef | grep php```
