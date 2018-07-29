# Flume-spark-streaming-Kafka

# Ubuntu 18.04下安装Flume+Spark Streaming +_Kafka

## 1 安装Flume
### 1.1 安装jdk 1.8
具体步骤见 ubuntu 下软件安装 jdk1.8安装。[See this](https://github.com/tytttta/Ubuntu/blob/master/%E8%BD%AF%E4%BB%B6%E5%AE%89%E8%A3%85.md)


## 2、下载flume

从官网下载压缩包：http://flume.apache.org/download.html

或

选择apache-flume-1.8.0-bin.tar.gz，选择镜像地址开始下载，如：
wget http://mirrors.tuna.tsinghua.edu.cn/apache/flume/1.8.0/apache-flume-1.8.0-bin.tar.gz

**本人选择了第二种**

## 3、解压并安装

### 解压：tar -zxvf apache-flume-1.8.0-bin.tar.gz
 
### 安装：mv apache-flume-1.8.0-bin /opt/flume-1.8.0（放到想要安装的目录下,目录名保存为flume-1.8.0，如/opt）(可能会没有权限，加上sudo)
