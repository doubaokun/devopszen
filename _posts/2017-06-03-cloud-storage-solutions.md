---
layout: post
published: true
title: Open source and free small files storage choices
mathjax: false
featured: true
comments: false
headline: Open source and free small files storage choices in the cloud data center
categories: 
  - storage
tags: devops disk storage ceph glusterfs s3
---


The requirement of storage system for small files are:

* Efficient
* Safe
* Cheap
* Scalable
* Simplicity
* Compatibility
* High Availability

### Ceph

Ceph provides object storage which compatible with S3 interface, Block storage (RADOS Block Device) which are striped and replicated across multiple machines, and POSIX compatible network file system (Cephfs).

[https://ceph.com/](https://ceph.com/)

Single Node Ceph Install steps:

[http://palmerville.github.io/2016/04/30/single-node-ceph-install.html](http://palmerville.github.io/2016/04/30/single-node-ceph-install.html)

### Glusterfs

GlusterFS is a scalable network filesystem. Using common off-the-shelf hardware, you can create large, distributed storage solutions for media streaming, data analysis, and other data- and bandwidth-intensive tasks.

[https://www.gluster.org/](https://www.gluster.org/)

### Facebook haystack

Facebook uses Haystack Object Store to store over 15 billion photos. 

[https://code.facebook.com/posts/685565858139515/needle-in-a-haystack-efficient-storage-of-billions-of-photos/](https://code.facebook.com/posts/685565858139515/needle-in-a-haystack-efficient-storage-of-billions-of-photos/)

### OpenStack Swift

Swift is the OpenStack Object Store solution optimized for durability, availability, and concurrency.

[https://docs.openstack.org/developer/swift/](https://docs.openstack.org/developer/swift/)

### TFS

TFS is the photos storage project for small files such as photos.

[http://tfs.taobao.org/](http://tfs.taobao.org/)
[http://code.taobao.org/p/tfs/wiki/intro/](http://code.taobao.org/p/tfs/wiki/intro/)

### Beansdb

Beansdb is a distributed key-value storage system designed for large scale online system, aiming for high avaliablility and easy management. It took the ideas from Amazon's Dynamo, then made some simplify to Keep It Simple Stupid (KISS).

[https://github.com/douban/beansdb](https://github.com/douban/beansdb)

### BFS

The Baidu File System (BFS) is a distributed file system designed to support real-time applications.

[https://github.com/baidu/bfs](https://github.com/baidu/bfs)

### Fastdfs

FastDFS is an open source high performance distributed file system (DFS). It's major functions include: file storing, file syncing and file accessing, and design for high capacity and load balance.

[https://github.com/happyfish100/fastdfs](https://github.com/happyfish100/fastdfs)

### Cassandra FS

S3 like file system implemented based on Cassandra

[https://github.com/zjffdu/cassandra-fs](https://github.com/zjffdu/cassandra-fs)

### Pithos (based on Cassandra)

pithos is a daemon which provides an S3-compatible frontend for storing files in a Cassandra cluster.

[http://pithos.io/](http://pithos.io/)

### SeaweedFS

SeaweedFS is a simple and highly scalable distributed file system.

[https://github.com/chrislusf/seaweedfs/blob/master/README.md](https://github.com/chrislusf/seaweedfs/blob/master/README.md)
