# AFK
Ansible For K8s

### 介绍
  这是一个ansible学习项目，通过ansibel处理部署k8s的环境初始化。基本条件是拥有目标机器的普通用户ssh权限和sudo权限。

### 使用

######  1: 准备hosts文件
 ```shell
[master]
192.168.1.2 hostname=k8s-master
[node]
192.168.1.3 hostname=k8s-node1
192.168.1.4 hostname=k8s-node2

[vars:children]
master
node

[all:vars]
ansible_user=
ansible_password=
ansible_become_user=
ansible_become_password=
ansible_become_method=su
```

###### 2: 准备代理
*** if you don't need proxy, go "开始运行"***

这个环境可以在内网部署，联网部分使用代理链接到互联网
1：socks代理
2：http代理
如果网络链接状良好，可以取消这一部分

###### 3： 安装ansible和模块

```shell
# 安装ansible
sudo dnf install ansible -y 
# 安装角色
sudo dnf install rhel-system-roles
ansible-galaxy collection install community.crypto
```

###### 4： 开始运行剧本

  如果想要检测一下剧本文件是否存在明显语法错误，可以执行检测
```shell
ansible-ploybook --syntax-check commit_swaap.yml
```
开始执行部署
```shell
# use proxy
ansible-playbook commit_swap.yml
# no proxy
ansible-playbook commit_internet.yml
```




