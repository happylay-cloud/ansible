### 常用模块指令
#--------------------------------------------------------------------------------------
###### 1.ansible 命令格式：
````
ansible 主机清单中ip或分组名称 -m 模块 -a '参数'
````
###### 2.ping模块应用
````
ansible all -m ping
ansible all -m ping -o
````
###### 3.cron模块应用
````
每小时与时钟源同步一次
ansible all -m cron -a 'name="time-cron" job="ntpdate time1.aliyun.com" minute=0 hour=*/1'

查看定时任务
crontab -l

取消cron定时任务
ansible all -m cron -a "state=absent name='time-cron'"
````
###### 4.copy模块应用
````
ansible node -m copy -a "src=/etc/hosts dest=/etc/hosts"
ansible node -m copy -a "src=/root/test.txt backup=yes dest=/root group=root"
ansible all -m copy -a "src=/data/happylay.sh dest=/data mode=755 backup=yes"
````
###### 5.fetch模块应用-从客户端取文件至服务器
````
ansible node2 -m fetch -a "src=/root/happylay.sh dest=/data"

拉取文件 falt=yes 且 dest以/结尾,将使用源文件的基础名称
ansible node2 -m fetch -a "src=/data/happylay.sh dest=/data/ flat=yes"
````

###### 6.hostname模块应用
````
管理主机名
ansible node1 -m hostname -a "name=k8s-node1"
````
###### 7.yum模块应用
````
安装
ansible node -m yum -a "name=lrzsz state=latest"

删除
ansible node -m yum -a "state=removed name=lrzsz"
````
###### 8.file模块应用
````
设置文件属性
ansible all -m file -a "path=/root/happylay.txt owner=root mode=777"

设置软连接
ansible all -m file -a "src=/root/happylay.txt dest=/data/happylay.txt state=link"
````
###### 9.command模块应用(默认)
````
查看文件夹
ansible all -m command -a "ls"

查看创建的任务计划
ansible all -m command -a 'crontab -l'

查看网卡信息
ansible all -m command -a 'ifconfig'

查看时间
ansible all -a date
````
###### 10.shell模块应用
````
打印
ansible all -m shell -a "echo 'hello world'"

查看主机名
ansible all -m shell -a 'echo $hostname'
ansible all -m shell -a 'hostname'
````
###### 11.script模块应用
````
ansible all -m script -a "/data/happylay.sh"
````
###### 12.查看模块列表
````
ansible-doc -l 
````
###### 13.查看模块的详细帮助信息
````
ansible-doc -s 模块
ansible-doc -s fetch
````
#---------------------------------PlayBook[剧本]---------------------------------------
````
# 
echo '
---
# 指定主机
- hosts: all
  # 指定在被管理的主机上执行任务的用户            
  remote_user: 'root'           
  tasks:
    # 任务列表                                         
    - name: hello world 
      # 调用command模块          
      shell: 'echo "hello world">/data/hello.txt'
' > helloworld.yml
````
````
检查yml文件的语法是否正确
ansible-playbook helloworld.yml --syntax-check

检测tasks任务
ansible-playbook helloworld.yml --list-task

检查生效的主机
ansible-playbook helloworld.yml --list-hosts

指定从某个task开始运行
ansible-playbook helloworld.yml --start-at-task='hello world'

执行任务
ansible-playbook helloworld.yml
````
#--------------------------------------------------------------------------------------





