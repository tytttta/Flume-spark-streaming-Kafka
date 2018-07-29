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

## 4、配置

修改配置文件：vi /opt/flume-1.8.0/conf/flume.conf

修改内容为：
````
agent1.souces=s1 s2
agent1.channels=c1
agent1.sinks=k1

agent1.sources.s1.type=spooldir
agent1.sources.s1.spoolDir=/data/log
agent1.sources.s1.channels=c1

agent1.sources.s2.type=avro
agent1.sources.s2.bind=0.0.0.0
agent1.sources.s2.ports=80
agent1.sources.s2.channel=c1

agent1.channels.c1.type=memory
agent1.channels.c1.capacity=1000
agent1.channels.c1.trasactionCapacity=100

agent1.sinks.k1.type=logger
agent1.sinks.k1.channel=c1
````

此配置文件，配置了两个source:s1和s2，一个channel，一个sink。s1监听目录/data/log目录，并把信息写入c1，s2监听本机所有ip(0.0.0.0)的80端口，信息也写入c1,k1从c1读取数据，写入flume的日志。 【具体说明见】(https://segmentfault.com/a/1190000011881177)

## 5、启动
````
/opt/flume-1.8.0/bin/flume-ng agent --conf conf --conf-file conf/flume.conf --name agent1 -Dflume.root.logger=INFO,console
````
- 启动命令参数说明：

参数|作用 |举例
----|-----|------
–conf 或 -c|指定配置文件夹，包含flume-env.sh和log4j的配置文件|–conf conf
–conf-file 或 -f 	| 配置文件地址|--conf-file conf/flume.conf
–name 或 -n|agent(flume节点)名称|--name agent1


**启动时可能会有警告，说JAVA_HOME未配置**
