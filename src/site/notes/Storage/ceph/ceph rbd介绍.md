---
{"dg-publish":true,"permalink":"/Storage/ceph/ceph rbd介绍/","noteIcon":"3","created":"","updated":""}
---

reference articles:
https://www.intel.com/content/www/us/en/developer/articles/technical/performance-tuning-of-ceph-rbd.html
https://www.youtube.com/watch?v=UjpaZ-JH4Yo

![Pasted image 20231019002305.png](/img/user/pics/Pasted%20image%2020231019002305.png)
## osds storing data
- ceph osd daemons存储数据作为objects以一个flat namespace(没有层级目录)，一个object含有一个identifier，binary data和包含一系列的name/value pair的metadata
- 数据和元数据使用bluestore,memorystore和seastore(在开发完善中)存储
- 元数据默认使用rocksdb(bluestore没有自己的元数据管理程序)存储，单独一个分区来存储元数据可以提升性能

Mapping PGs to OSDs
- 客户端存储objects时，crush会将objects map到PG上
- 每一个pool有一些pgs， crush会动态的将pgs map到osds

## client-RBD IO Layer
逐层下发

ImageDispatchLayer
ObjectDispatchLayer

## Threads Model
![Pasted image 20231019002342.png](/img/user/pics/Pasted%20image%2020231019002342.png)