#### gitlab 安装
#### 1.安装centos 7
#### 2.打开清华源下载  安装包
            https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el7/
```
目录路径： /gitlab-ce/yum/el7/
```
#### 2.1.yum install -y [安装包]
![image](/upload/2022/10/image.png)#### 4. 

##### 安装过程中有可能会卡住 使用一下解决方案
（1）重新再开一个终端，并执行以下命令
```shell
/opt/gitlab/embedded/bin/runsvdir-start
```
（2）或在当前终端使用以下命令，再初始化
```shell

#后台运行runsvdir-start程序
/opt/gitlab/embedded/bin/runsvdir-start &
然后再运行
gitlab-ctl reconfigure

```
（3）再或者CTRL+C强行终止，再运行以下命令(这个方法没验证过，不知道行不行)
```shell

#1.先运行这个
systemctl restart gitlab-runsvdir
#2.再运行
gitlab-ctl reconfigure
```