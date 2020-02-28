# docker-compose一键搭建简易redis哨兵集群  

## 说明  
本项目为最简易的1主2从3哨兵架构，仅供新手学习  
服务器需开放6个端口7000、7001、7002、26379、26380、26381  
其中7000为主节点，7001、7002为从节点  
data7000、data7001、data7002分别为三台主从节点存放持久化文件及日志的目录  
sentinel26379、sentinel26380、sentinel26381分别为三台哨兵节点存放日志的目录  

## 修改文件  
分别修改文件docker-compose.yml、sentinel26379.conf、sentinel26380.conf、sentinel26381.conf中的**x.x.x.x**为你的服务器IP  

## 启动集群  
docker-compose up -d  

## 故障自动转移测试  
关闭主节点：docker rm -f redis-master  
查看哨兵日志，可以找到已选举出新master节点的日志记录  
登录新master节点redis，执行**info**命令验证是否为master身份  

## 关闭集群  
docker-compose down

## 注意事项
测试过一次故障转移后，重新启动老master他会以从节点的身份链接到新master，再次测试故障转移需要关闭的是新master，所以测试前最好用info命令确认哪个才是master
