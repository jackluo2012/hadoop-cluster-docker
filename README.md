##Run Hadoop Custer within Docker Containers
如果觉得太慢，可以先下载到本地
http://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-2.7.2/hadoop-2.7.2.tar.gz
放到 hadoop-cluster-docker目录里面:
```
ackluo@jackluo-X550CC:/works/hadoop-cluster-docker$ ls
Dockerfile  README.md  build-image.sh  config  hadoop-2.7.2.tar.gz  resize-cluster.sh  start-container.sh
```
博客: [基于Docker搭建Hadoop集群之升级版](http://kiwenlau.com/2016/06/12/160612-hadoop-cluster-docker-update/)


![alt tag](https://raw.githubusercontent.com/kiwenlau/hadoop-cluster-docker/master/hadoop-cluster-docker.png)


###3 Nodes Hadoop Cluster


#####1. clone github repository

```
git clone https://github.com/kiwenlau/hadoop-cluster-docker
```

#####2. build docker image

```
cd hadoop-cluster-docker
wget http://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/common/hadoop-2.7.2/hadoop-2.7.2.tar.gz
sudo sh build-image.sh
```


#####3. create hadoop network

```
sudo docker network create --driver=bridge hadoop
```

#####4. start container

```
sudo ./start-container.sh
```

**output:**

```
start hadoop-master container...
start hadoop-slave1 container...
start hadoop-slave2 container...
root@hadoop-master:~# 
```
- start 3 containers with 1 master and 2 slaves
- you will get into the /root directory of hadoop-master container

#####5. start hadoop

```
./start-hadoop.sh
```

#####6. run wordcount

```
./run-wordcount.sh
```

**output**

```
input file1.txt:
Hello Hadoop

input file2.txt:
Hello Docker

wordcount output:
Docker    1
Hadoop    1
Hello    2
```

###Arbitrary size Hadoop cluster

#####1. pull docker images and clone github repository

do 1~2 like section A

#####2. rebuild docker image

```
./resize-cluster.sh 5
```
- specify parameter > 1: 2, 3..


#####3. start container

```
./start-container.sh 5
```
- use the same parameter as the step 2

#####4. run hadoop cluster 

do 3~5 like section A

