# ansible
自动化运维工具使用指南

#### 自动化运维ansible-pull高级用法
````
 ansible-pull -U https://github.com/happylay-cloud/ansible.git -d /data/happylay playbook/helloworld.yml --limit all
 
 ansible-pull -C v0.0.1 -U https://github.com/happylay-cloud/ansible.git -d /data/happylay playbook/helloworld.yml --limit all -o
````
#### 参数说明
| 参数| 说明| 
|:-|:-|
|-U|仓库地址|
|-d| 目标文件夹(必须为空)|
|--limit|主机清单(关键)|
|-o|代码库更新时执行剧本|
|-C|代码版本 分支/标签|
