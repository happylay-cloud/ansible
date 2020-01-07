# ansible
自动化运维工具使用指南

#### 自动化运维ansible-pull高级用法
````
 ansible-pull -U https://github.com/happylay-cloud/ansible.git -d /data/happylay playbook/helloworld.yml --limit all
````
#### 参数
````
-U       仓库地址
-d       目标文件夹
--limit  主机清单(关键)
````