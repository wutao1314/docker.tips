在 Linux 系统上安装 Docker
================================
# 一.CentOS7 安装Docker
## 方法1
	#此方法可以安装，也可以升级docker
	curl -sSL get.docker.com | sh
## 方法2
	#此方法需确保系统内没有安装docker，如果已经安装docker，需要先卸载docker。
	#卸载方法详见卸载
	sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
# 二、CentOS7 卸载Docker
	sudo yum remove docker \                                                              
	                  docker-client \                                                                                        
	                   docker-client-latest \                                                                                        
	                   docker-common \                                                                                                 
	                   docker-latest \                                                                                                
	                   docker-latest-logrotate \                                                                                         
	                   docker-logrotate \                                                                                                
	                   docker-engine  
	#为了确保删除干净，可在执行
	sudo yum remove docker*
	#删除目录
	rm -rf /var/lib/docker/
# 三、配置registry-mirrors
**此步骤可以省略。**
由于hub.docker.com官网镜像，国内连接不稳定。可以配置其他镜像源
```python
#创建或打开daemon.json文件
vi /etc/docker/daemon.json
#按i进入insert模式，写入的内容如下，按ESC退出insert模式，输入:wq 回车保存
{
  "registry-mirrors":[
    "https://registry.docker-cn.com",
    "https://hub-mirror.c.163.com",
    "https://docker.mirrors.ustc.edu.cn"
    ],
  "dns":[
    "8.8.8.8",
    "114.114.114.114"
    ]
}
```
# 四、加载配置
配置完registry-mirrors需重新加载配置。
```python
#加载配置
systemctl daemon-reload
#重启配置生效
systemctl restart docker
```
# 五、查看Docker信息
```python
#查看docker版本
docker version
#查看docker详细信息
docker info
```
笔记地址：https://dockertips.readthedocs.io/
