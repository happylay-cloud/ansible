# ansible-2.9.2
自动化运维工具使用指南 | [常用模块](doc/README.md)

#### 1.在线安装
````
curl -ssl https://raw.githubusercontent.com/happylay-cloud/ansible/master/install/run.sh | sh
````
#### 2.自动化运维ansible-pull高级用法
````
 ansible-pull -U https://github.com/happylay-cloud/ansible.git -d /data/happylay playbook/helloworld.yml --limit all
 
 ansible-pull -C v0.0.1 -U https://github.com/happylay-cloud/ansible.git -d /data/happylay playbook/helloworld.yml --limit all -o
 
 ansible-pull -C master -U https://github.com/happylay-cloud/ansible.git -d /data/happylay playbook/helloworld.yml --limit all -o
 
 ansible-pull -C v0.0.2 -U https://github.com/happylay-cloud/ansible.git -d /data/happylay playbook/helloworld.yml --limit all -o >> /data/happylay/ansible-pull.log 2>&1
````
#### 3.参数说明
| 参数| 说明| 
|:-|:-|
|-U|仓库地址|
|-d| 目标文件夹(必须为空)|
|--limit|主机清单(关键)|
|-o|代码库更新时执行剧本|
|-C|代码版本 分支/标签|
#### 4.定时任务
````
root用户计划每分钟检查仓库代码,代码更新后执行剧本并记录日志
ansible master -m cron -a " name='ansible-pull' minute=*/1 hour=* day=* month=* weekday=* job='ansible-pull -C v0.0.2 -U https://github.com/happylay-cloud/ansible.git -d /data/happylay playbook/helloworld.yml --limit all -o >> /data/happylay/ansible-pull.log 2>&1' user=root "
````
#### 5.查看创建的任务
````
ansible all -m command -a 'crontab -l'
````
#### 6.取消定时任务
````
ansible master -m cron -a "state=absent name='ansible-pull'"
````
