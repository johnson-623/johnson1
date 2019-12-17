# 大作业报告

说明：所用的设备是mac且由于其他课程需要已经安装了windows虚拟机，碍于存储空间选择了使用docker完成本次的大作业。
---

## 安装docker并搭建nebula环境：   
使用docker创建nebula graph:    
注册docker账号    
依照流程先后进行了命令：docker pull vesoft/nenula-graph     
![image](https://github.com/johnson-623/johnson1/blob/master/images/1.png)

---
pull操作完成：   
![image](https://github.com/johnson-623/johnson1/blob/master/images/2.png)

---
启动容器并cd到nebula所在的目录下：    
![image](https://github.com/johnson-623/johnson1/blob/master/images/3.png)
---
启动所有的nebula服务：    
![image](https://github.com/johnson-623/johnson1/blob/master/images/4.png)

---
通过console链接数据库：    
![image](https://github.com/johnson-623/johnson1/blob/master/images/5.png)

---
创建三个tag和两个edge：    
![image](https://github.com/johnson-623/johnson1/blob/master/images/6.png)
### *至此为止，nebula已可以正常运行*    
   
---
## 错误的发现以及对错    
但是当我运行脚本.sh文件时遇到报错：“unkown system”  
原因：分析脚本代码后发现该脚本是基于ubuntu编写的，在mac环境下无法正常运行    
![image](https://github.com/johnson-623/johnson1/blob/master/images/7.png)   

---
分析脚本代码后，利用brew先后安装了rpm后，考虑到脚本的信息量对我而言过于庞大，选择借用同学搭载了ubuntu系统的电脑进一步进行学习。    
![image](https://github.com/johnson-623/johnson1/blob/master/images/8.png)    

---
## 借用电脑后在ubuntu系统下继续完成大作业    

