# docker-compose一键搭建简易redis哨兵集群

【说明】
本项目为最简易的1主2从3哨兵架构，仅供新手学习
服务器需开放6个端口7000、7001、7002、26379、26380、26381
其中7000为主节点，7001、7002为从节点
data7000、data7001、data7002分别为三台主从节点存放持久化文件及日志的目录
sentinel26379、sentinel26380、sentinel26381分别为三台哨兵节点存放日志的目录

【修改文件】
分别修改docker-compose.yml、sentinel26379.conf、sentinel26380.conf、sentinel26381.conf中的x.x.x.x为你的服务器IP

【启动集群】
cd redis-sentinel
docker-compose up -d

【故障转移测试】
故意关闭主节点：docker rm -f redis-master
查看哨兵日志，可以找到已选举出新master节点的日志记录
登录新master节点redis，执行info命令验证是否为master身份

【关闭集群】
docker-compose down
