# 大作业报告

说明：所用的设备是mac且由于其他课程需要已经安装了windows虚拟机，碍于存储空间选择了使用docker完成本次的大作业。
---

## 安装docker并搭建nebula环境：   
使用docker创建nebula graph:    
注册docker账号    
依照流程先后进行了命令：docker pull vesoft/nenula-graph     
![image](https://github.com/johnson-623/johnson1/blob/master/images/截屏2019-12-17下午2.00.34.png)

---
pull操作完成：
[image:4242AD8F-4940-4C1D-A178-99FDD0FDACE9-4459-00000E3C4EE57134/截屏2019-12-17下午2.07.35.png]

---
启动容器并cd到nebula所在的目录下：
[image:14A50265-2BE9-4AEA-B3AA-073667F1AA3D-4459-00000E5B1E9DF29E/截屏2019-12-17下午2.09.49.png]

---
启动所有的nebula服务：
[image:0AC9C89D-7D32-4397-B265-29139871A9C2-4459-00000E8FB4F287C6/截屏2019-12-17下午2.13.35.png]

---
通过console链接数据库：
[image:FF5FAE21-D8B6-4E3C-B6E5-03B888DA73CB-4459-00000E9D198CEDA4/截屏2019-12-17下午2.14.33.png]

---
创建三个tag和两个edge：
[image:8E732D35-415B-4F35-989C-FA58BAAD57FB-4459-00000F7E9ACA1121/截屏2019-12-17下午2.30.28.png]

### *至此为止，nebula已可以正常运行*

---
## 错误的发现以及对错
但是当我运行脚本.sh文件时遇到报错：“unkown system”
原因：分析脚本代码后发现该脚本是基于ubuntu编写的，在mac环境下无法正常运行
[image:8B1C6C2B-F1C8-49DA-83F7-0A2C87D50354-4459-000018981FB88711/截屏2019-12-17下午3.04.44.png]
---
分析脚本代码后，利用brew先后安装了rpm后，考虑到脚本的信息量对我而言过于庞大，选择借用同学搭载了ubuntu系统的电脑进一步进行学习。
[image:16369577-62D3-4685-87A3-90FCE8C84F3C-4459-00001906C7E5653F/截屏2019-12-17下午8.59.54.png]
---
## 借用电脑后在ubuntu系统下继续完成达作业

