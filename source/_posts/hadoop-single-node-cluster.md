---
title: Hadoop Single Node Cluster 的安装
date: 2019-11-15 23:39:05
categories: Hadoop
tags:
- install
- hadoop
---
1. 安装 JDK

    - 使用 apt-get 安装 JDK

    ```bash
    sudo apt-get install default-jdk
    ```

    - 查询 Java 版本

    ```bash
    java -version
    ```

    - 查询 Java 安装路径

    ```bash
    update-alternatives --display java
    ```

2. 设置 SSH 无密码登陆

    - 安装 SSH

    ```bash
    sudo apt-get install ssh
    ```

    - 产生 SSH Key

    ```bash
    ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
    ```

    - 将产生的 Key 放置到许可证文件在中

    ```bash
    cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
    chmod 0600 ~/.ssh/authorized_keys
    ```

    - 安装 openssh-server

    ```bash
    sudo apt-get install openssh-server
    ```

    - 查看是否安装成功

    ```bash
    ps -e|grep ssh
    ```

3. 下载安装 Hadoop

    - 到 [官网]( https://hadoop.apache.org/releases.html ) 复制下载链接
    - 执行下载命令

    ```bash
    wget http://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/common/hadoop-2.10.0/hadoop-2.10.0.tar.gz
    ```

    - 解压缩

    ```bash
    sudo tar -zxvf hadoop-2.10.0.tar.gz
    ```

    - 将 Hadoop 移动到 `/usr/local`

    ```bash
     sudo mv hadoop-2.10.0 /usr/local/hadoop
    ```

    - 查看 Hadoop 安装目录 `/usr/local/hadoop`

    ```bash
    ll /usr/local/hadoop
    ```

4. 设置 Hadoop 环境变量

    - 修改 `~/.bashrc`, 添加以下内容

    ```bash
    # 设置JDK安装路径
    export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
    # 设置Hadoop安装路径
    export HADOOP_HOME=/usr/local/hadoop
    # 设置PATH
    export PATH=$PATH:$HADOOP_HOME/bin
    export PATH=$PATH:$HADOOP_HOME/sbin
    # 设置Hadoop其他环境变量
    export HADOOP_MAPRED_HOME=$HADOOP_HOME
    export HADOOP_COMMON_HOME=$HADOOP_HOME
    export HADOOP_HDFS_HOME=$HADOOP_HOME
    export YARN_HOME=$HADOOP_HOME
    # 链接库的相关设置
    export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
    export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib"
    export JAVA_LIBRARY_PATH=$HADOOP_HOME/lib/native:$JAVA_LIBRARY_PATH
    ```

    - 让 `~/.bashrc` 设置生效

    ```bash
    source ~/.bashrc
    ```

5. 修改 Hadoop 配置设置文件

    - 编辑 `hadoop-dev.sh`

    ```bash
    sudo gedit /usr/local/hadoop/etc/hadoop/hadoop-env.sh
    ```

    ```sh
    export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
    ```

    - 修改 `core-site.xml`

    ```bash
    sudo gedit /usr/local/hadoop/etc/hadoop/core-site.xml
    ```

    ```xml
    <configuration>
        <property>
            <name>fs.defaultFS</name>
            <value>hdfs://localhost:9000</value>
        </property>
    </configuration>
    ```

    - 修改 `hdfs-site.xml`

    ```bash
    sudo gedit /usr/local/hadoop/etc/hadoop/hdfs-site.xml
    ```

    ```xml
    <configuration>
        <property>
            <name>dfs.replication</name>
            <value>3</value>
        </property>
        <property>
            <name>dfs.namenode.name.dir</name>
        <value>file:/usr/local/hadoop/hadoop_data/hdfs/namenode</value>
        </property>
        <property>
            <name>dfs.datanode.data.dir</name>
            <value>file:/usr/local/hadoop/hadoop_data/hdfs/datanode</value>
        </property>
    </configuration>
    ```

    - 创建并格式化 HDFS 目录

    ```bash
    # 创建namenode数据存储目录
    sudo mkdir -p /usr/local/hadoop/hadoop_data/hdfs/namenode
    # 创建datanode数据存储目录
    sudo mkdir -p /usr/local/hadoop/hadoop_data/hdfs/datanode
    # 将数据所有者更改为hduser
    sudo chown hduser:hduser -R /usr/local/hadoop
    # 格式化namenode
    hadoop namenode -format
    ```

    - 启动 HDFS

    ```bash
    start-dfs.sh
    ```

    - 修改 `yarn-site.xml`

    ```bash
    sudo gedit /usr/local/hadoop/etc/hadoop/yarn-site.xml
    ```

    ```xml
    <configuration>
        <property>
            <name>yarn.nodemanager.aux-services</name>
            <value>mapreduce_shuffle</value>
        </property>
        <property>
            <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
            <value>org.apache.hadoop.mapred.ShuffleHandler</value>
        </property>
    </configuration>
    ```

    - 设置 `mapred-site.xml`

    ```bash
    sudo cp /usr/local/hadoop/etc/hadoop/mapred-site.xml.template /usr/local/hadoop/etc/hadoop/mapred-site.xml
    sudo gedit /usr/local/hadoop/etc/hadoop/mapred-site.xml
    ```

    ```xml
    <configuration>
        <property>
            <name>mapreduce.framework.name</name>
            <value>yarn</value>
        </property>
        <property>
            <name>mapreduce.application.classpath</name>
            <value>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*:$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</value>
        </property>
    </configuration>
    ```

    - 启动 YARN

    ```bash
    start-yarn.sh
    ```

    - 同时启动 HDFS 和 YARN

    ```bash
    start-all.sh
    ```

    - 查看已启动的进程

    ```bash
    jps
    ```

    - HDFS 功能
      - NameNode
      - SecondaryNameNode
      - DataNode
    - MapReduce2(YARN)
      - ResourceManager
      - NodeManager

6. 打开 Hadoop Resource-Manager Web 界面

    [localhost:8080](http://localhost:8088/)

参考

- [Setting up a Single Node Cluster](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/SingleCluster.html#Installing_Software)
- [Hadoop 2.6 Single Node Cluster 安裝指令](http://blog.sina.com.cn/s/blog_1618db3120102w7wa.html)