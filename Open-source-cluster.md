# Open-source-cluster
## Deployment details

hadoop

			   hadoop102 	    hadoop103	    hadoop104
	 HDFS   
			   NameNode
			   DataNode	
			   		    DataNode	    SecondaryNameNode
			   				    DataNode
	  YARN	   
			   NodeManager	    ResourceManager
				   	    NodeManager	
				   			    NodeManager		   
-------------------------------
zookeeper

			   hadoop102	    hadoop103	     hadoop104
			   Zookeeper	    Zookeeper	     Zookeeper

-------------------------------
kafka

			   hadoop102	     hadoop103	    hadoop104
			   √            	√             	√  

--------------------------------
flume

```
			hadoop102	    hadoop103	    hadoop104
    			√               	√
```

-------------------------------
clickhouse

```
			hadoop102	    hadoop103	    hadoop104
      			√            		√             	√  	     
```

-------------------------------
hbase

```
			hadoop102	    hadoop103	    hadoop104
      			√             		√             	√        
```

-------------------------------
maxwell 

```
			hadoop102	    hadoop103	    hadoop104
      			√             		√             	√
```

-------------------------------
phoenix

```
			hadoop102	    hadoop103	    hadoop104
      			√                            
```

-------------------------------
mysql 

```
			hadoop102	    hadoop103	    hadoop104
      			√                       
```

-------------------------------
flink 

```
			hadoop102	    hadoop103	    hadoop104
      			JobManager    	    TaskManager     TaskManager             
```

-------------------------------
redis 

```
			hadoop102	    hadoop103	    hadoop104
      			√  
```

​      
​      





## Cluster startup & shutdown command

### hdfs&yarn&historyserver

```
群启/停脚本 hdp.sh     参数：start & stop
```



### zookeeper

```
群启/停脚本 zk.sh      参数：start & stop & status
```



### Kafka

```
集群启停脚本 kafka.sh   参数：start & stop
```



### hive

```
群启/停
	方式1：hive 客户端
			启动命令： hive
			退出命令： quit;
			
	方式2：beeline 客户端 (需开启hiveserver2服务)
			启动命令： beeline -u jdbc:hive2://hadoop102:10000 -n hadoop
			退出命令： !quit
```



### mysql

```
 启动MySQL服务： sudo systemctl start mysqld
 
 查看MySQL状态： service mysqld status
 
 登录MySQL数据库： mysql -u root -p000000
```



### flink

```
 群启/停(Standalone Session Mode)
 服务脚本 
 	flink.sh  参数：start & stop
    
 客户端
 	a.WEB UI界面提交任务
 		http://hadoop102:8081
 	b.命令行提交作业
 		bin/flink run -m hadoop102:8081 -c com.hadoop.wc.StreamWordCount ./FlinkTutorial-1.0-SNAPSHOT.jar
 		*这里的参数 –m 指定了提交到的JobManager，-c 指定了入口类。
 		在hadoop102中执行以下命令启动netcat
		nc -lk 7777
		*用netcat输入数据，可以在TaskManager的标准输出（Stdout）看到对应的统计结果
```



### hbase

```
 群启/停
 服务脚本
    hbase.sh  参数：start & stop

 客户端 
	启动命令： hbase shell
	退出命令： quit
	
 WEB UI界面
 	http://hadoop102:16010 
```

### phoenix

```
群启/停 
/opt/module/phoenix/bin/sqlline.py hadoop102,hadoop103,hadoop104:2181 
```

### flume

```
集群启停脚本 flume.sh    参数：start & stop
```

### maxwell

```
集群启停脚本 maxw.sh     参数：start & stop & restart
```

### redis      

```
	默认安装路径：/usr/local/bin/
	
	启动
	redis-server /usr/local/bin/redis.conf
	关闭
		客户端内：shutdown
		客户端外：redis-cli shutdown
				redis-cli -p 6379 shutdown  （多端口关cli -p指定端口）	
	
	
	客户端：redis-cli
		   redis-cli -p 6379 （多端口起cli -p指定端口）
	查看进程：ps -ef | grep redis
	验证：  127.0.0.1:6379> ping
		   PONG
```

### clickhouse

```
 群启/停
 服务
 	sudo systemctl start clickhouse-server
 	sudo systemctl stop clickhouse-server
 客户端
 	clickhouse-client -m
	quit

```

