---
layout: mypost
title: 存储基础知识
categories: [教程]
extMath: false
---

##### 什么是存储
存储是数据的载体，负责数据高性能的存取。是一个可以通过一堆不可靠，性能有限，容量小的硬盘构建出高可靠，高性能，大容量的专业存储系统的一个软硬件一体的设备。

##### 存储的分类

- 块存储（SAN）
以块存储提供服务的设备叫SAN(Storage Area Network)存储。块存储用于存储结构化数据，即通过读写存储空间中的一个或多个地址直接读写数据。这种直接访问的方式是的块存储的开销最小，效率最高。同时产生了成本高，扩展性不强的问题。常用于对I/O性能敏感的场景，如Oracle数据库、Vmware虚拟化等。
- 文件存储(NAS)
以文件存储提供服务的设备叫NAS(Network-Attached Storage)存储。文件存储主要用于存储非结构化数据。通过在块存储设备上添加专业文件系统，实现文件共享。文件存储易于管理,易于共享，即插即用，虽然支持扩展，但生态兼容性要求较多，权限复杂，树状结构使得访问效率偏低。常用于企业内部应用集成、文件共享等场景。
- 对象存储(OBS)
以对象存储提供服务的设备叫S3存储。对象存储是一种网络存储架构。OBS与块存储或文件存储的区别主要在于OBS提供的接口（S3接口）。OBS只为存储数据的元数据生成一个ID，并存储该ID，不管数据类型如何。主要应用于对性能要求不高，但对容量要求较高的场景。扁平化的结构，使容量几乎可以无限扩展。

##### NAS与SAN：差异与应用场景

NAS和SAN这两种存储架构相互补充，因为它们具有竞争力，可以满足组织中的不同需求和使用情况。但是，企业IT预算不是无限的，组织需要优化其存储支出以适应其优先级要求。本文将通过定义NAS和SAN，找出它们的区别以及介绍两种体系结构的使用场景。


###### 7大差异

|   -    |NAS    |SAN   |
|----------|--------|----|
| 结构    |使用TCP / IP网络      |在高速光纤通道网络上运行   |
| 数据处理 |处理基于文件的数据      |处理块数据   |
| 协议    |直接连接到以太网,可以使用多种协议与服务器连接，包括NFS，SMB / CIFS和HTTP      |使用SCSI协议与服务器通信|
| 性能    |由于文件系统层较慢，因此通常具有较低的吞吐量和较高的延迟      |对于需要高速流量的环境，性能更高|
| 可拓展性 |入门级和NAS设备的扩展性不高，高端NAS系统使用群集或横向扩展节点可扩展至PB     |可扩展性是主要驱动力：其网络架构使管理员能够在向上或向外扩展配置中扩展性能和容量  |
| 可维护性 |易于管理：设备轻松插入局域网并提供简化的管理界面      |比NAS需要更多的管理时间  |
| 价格    |通常高端NAS的购买和维护成本较低，尽管高端NAS的成本将高于入门级SAN。      |在复杂性堆之上，使用FC SAN管理SAN更为复杂  |


###### 使用场景

**NAS：当需要整合，集中和共享时**

- 文件存储和共享。这是中型，SMB和企业远程办公中NAS的主要使用场景。单个NAS设备允许IT部门整合多个文件服务器，以简化操作，简化管理并节省空间和能源。

- 活动档案。长期归档最好存储在价格较低的存储设备中，例如磁带或基于云的冷存储设备。NAS是可搜索和可访问的活动归档的理想选择，大容量NAS可以代替大型磁带库进行归档。

- 大数据。企业可以选择大数据：横向扩展NAS，分布式JBOD节点，全闪存阵列和基于对象的存储。横向扩展NAS非常适合处理大文件，ETL（提取，转换，加载），智能数据服务（例如自动分层）和分析。对于大型非结构化数据（例如，视频监控和流传输以及后期制作存储），NAS也是一个不错的选择。

- 虚拟化。并非所有人都可以将NAS用于虚拟化网络，但是使用案例在不断增长，VMware和Hyper-V都支持NAS上的数据存储。当企业尚未拥有SAN时，对于新的或小型虚拟化环境，这是一个流行的选择。

- 虚拟桌面界面（VDI）。中高端NAS系统提供支持VDI的本机数据管理功能，例如快速桌面克隆和重复数据删除。

**SAN：需要加速，扩展和保护时**
- 数据库和电子商务网站。常规文件服务或NAS将适用于较小的数据库，但是高速事务环境需要SAN的高I / O处理速度和极低的延迟。这使得SAN非常适合企业数据库和高流量电子商务网站。

- 快速备份。服务器操作系统将SAN视为附加存储，从而可以快速备份到SAN。由于服务器直接备份到SAN，因此备份流量不会通过LAN传输。这样可以加快备份速度，而又不增加以太网的负载。

- 虚拟化。NAS支持虚拟化环境，但SAN更适合大规模和/或高性能部署。存储区域网络可在VM和虚拟化主机之间快速传输多个I / O流，并且高可伸缩性可实现动态处理。

- 视频编辑。视频编辑应用程序需要非常低的延迟和非常高的数据传输速率。SAN之所以具有这种高性能，是因为它直接连接到视频编辑桌面客户端，而无需额外的服务器层。视频编辑环境需要第三方SAN分布式文件系统和每个节点的负载平衡控制。


##### RAID介绍

###### 什么是 RAID
冗余磁盘阵列技术RAID(Redundant Array of Inexpensive Disks)最初的研制目的是为了组合小的廉价磁盘来代替大的昂贵磁盘，以降低大批量数据存储的费用，同时也希望采用冗余信息的方式，使得磁盘失效时不会使对数据的访问受损失，从而开发出一定水平的数据保护技术，并且能适当的提升数据传输速度。

过去RAID一直是高档服务器才有缘享用，一直作为高档SCSI硬盘配套技术作应用。近来随着技术的发展和产品成本的不断下降，IDE硬盘性能有了很大提升，加之RAID芯片的普及，使得RAID也逐渐在个人电脑上得到应用。

那么为何叫做冗余磁盘阵列呢？冗余的汉语意思即多余，重复。而磁盘阵列说明不仅仅是一个磁盘，而是一组磁盘。这时你应该明白了，它是利用重复的磁盘来处理数据，使得数据的稳定性得到提高。

###### 为什么用 RAID
1) 扩大了存储能力，可由多个硬盘组成容量巨大的存储空间。
2) 降低了单位容量的成本，市场上最大容量的硬盘每兆容量的价格要大大高于普及型硬盘，因此采用多个普及型硬盘组成的阵列其单位价格要低得多。
3) 提高了存储速度 单个硬盘速度的提高均受到各个时期的技术条件限制，要更进一步往往是很困难的，而使用 RAID，则可以让多个硬盘同时分摊数据的读或写操作，因此整体速度有成倍地提高。
4) 可靠性 RAID 系统可以使用两组硬盘同步完成镜像存储，这种安全措施对于网络服务器来说是最重要不过的了。
5) 容错性 RAID 控制器的一个关键功能就是容错处理。容错阵列中如有单块硬盘出错，不会影响到整体的继续使用，高级 RAID 控制器还具有拯救数据功能。

###### RAID等级
RAID等级的选择主要有三个因素，即数据可用性、 I/O 性能和成本。

目前，在实际应用中常见的主流 RAID 等级是
- RAID0
- RAID1
- RAID3
- RAID5
- RAID6
- RAID10

如果不要求可用性，选择 RAID0 以获得高性能。如果可用性和性能是重要的，而成本不是一个主要因素，则根据磁盘数量选择 RAID1 。如果可用性，成本和性能都同样重要，则根据一般的数据传输和磁盘数量选择 RAID3 或 RAID5 。在实际应用中，应当根据用户的数据应用特点和具体情况，综合考虑可用性、性能和成本来选择合适的 RAID 等级。

**主流 RAID 等级技术对比**

| RAID等级  | RAID0  | RAID1  | RAID3  | RAID5  | RAID6  | RAID10  |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| 别名  | 条带  | 镜像  | 专用奇偶校验条带  | 分布奇偶校验条带  | 双重奇偶校验条带  | 镜像加条带  |
| 容错性  | 无  | 有  | 有  | 有  | 有  | 有  |
| 冗余类型  | 无  | 有  | 有  | 有  | 有  | 有  |
| 热备份选择  | 无  | 有  | 有  | 有  | 有  | 有  |
| 读性能  | 高  | 低  | 高  | 高  | 高  | 高  |
| 随机写性能  | 高  | 低  | 低  | 一般  | 低  | 一般  |
| 连续写性能  | 高  | 低  | 低  | 低  | 低  | 一般  |
| 需要磁盘数  | n≥1  | 2n (n≥1)  | n≥3  | n≥3 | n≥4  | 2n(n≥2)≥4  |
| 可用容量  | 全部  | 	50%  | (n-1)/n  | (n-1)/n  | (n-2)/n  | 50%  |

