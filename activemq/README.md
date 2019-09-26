## Dockerfile for ActiveMQ 5.15.10

Dockerfile构建过程中会下载ActiveMQ的bin-tar.gz，使用的链接为https://mirrors.tuna.tsinghua.edu.cn/apache/activemq/5.15.10/apache-activemq-5.15.10-bin.tar.gz，如有需要自行修改。

升级版本时，需要修改Dockerfile中的版本号和SHA512的值，具体的版本号与SHA512信息参考官网。

### 使用实例

- #### 构建image

```
 docker build -t activemq:5.15.10 . 
```

- #### 备份默认配置文件到挂载路径

首先启动一个容器，进入bash
```
docker run --user root --rm -ti \
  -v /your/persistent/dir/conf:/mnt/conf \
  -v /your/persistent/dir/data:/mnt/data \
  activemq:5.15.10 /bin/sh
```

在shell终端执行如下命令即可
```
chown activemq:activemq /mnt/conf
chown activemq:activemq /mnt/data
cp -a /opt/activemq/conf/* /mnt/conf/
cp -a /opt/activemq/data/* /mnt/data/
exit
```
完成后可以删除该临时容器

- #### 启动容器

参考端口信息
```
61616 JMS
8161  UI
5672  AMQP 
61613 STOMP
1883  MQTT 
61614 WS   
```

使用自定义配置文件，映射多有端口
```
docker run -d --name activemq51510 \ 
-p 61616:61616 -p 8161:8161 -p 5672:5672 \
-p 61613:61613 -p 1883:1883 -p 61614:61614 \
-v /your/persistent/dir/conf:/opt/activemq/conf \
-v /your/persistent/dir/data:/opt/activemq/data \
activemq:5.15.10
```

