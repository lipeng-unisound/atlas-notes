# 2016-05-07

* 完成了使用 iPXE 引导 CoreOS 的实验
  * 子网内没有 DHCP 服务，所以我自建了 DHCP 和 TFTP 服务，根据 [iPXE 的文档](http://ipxe.org/howto/chainloading) 通过 PXE 来 chainload iPXE 
  * 使用了 [coreos-ipxe-server](https://github.com/kelseyhightower/coreos-ipxe-server) 这个工具来引导安装 CoreOS 到内存。这个工具的方便在于：
    * 自动生成 iPXE boot script，通过自带的 HTTP 服务提供。
    * 可以为每台主机分别提供不同的 cloud-config 文件，通过 iPXE 提供的主机 MAC 地址自动选择，从而可以批量安装系统。
    * 一个 tip：iPXE 的变量 ${net0/mac} 替换为网卡 MAC 时是小写，如果 coreos-ipxe-server 的配置文件名用的是大写（如[这个视频](https://www.youtube.com/watch?v=dRG2ajUaBqs)中演示的），会找不到文件。
* TODO
  * 研究怎样继续把 CoreOS 安装到硬盘
    * cloud-config 的内容。systemd, fleet, etcd2 以及其他 units 是否需要在安装前就要全部配置好？安装之后就没有机会添加了？
    * 硬盘分区的问题。现在每台机有一块 1TB 硬盘，并做了 RAID0，观察安装 CoreOS 后是如何自动分区的（两个 1GB 的系统分区，其他的呢？）
    * 用户管理问题。cloud-config 中只提供一个 sshkey，安装完成后是否可以添加用户？


