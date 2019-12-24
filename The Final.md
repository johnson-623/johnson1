# 大作业报告
赵崇尚 18061138

说明：实现初期所用的设备是mac且由于其他课程需要已经安装了windows虚拟机，碍于存储空间选择了使用docker；
但由于依赖安装脚本不兼容mac版本的docker，实现后期更换了设备在ubuntu系统下完成本次大作业，虽然一波三折，但是颇有收获！
即nebula graph的正常运行时在mac环境下实现的；源代码的修改编译以及单元测试部分是在ubuntu系统中完成。

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

### git clone https://github.com/vesoft-inc/nebula ，网速较慢，但是过程非常顺利。
### 但是当我安装依赖的过程中出现报错“unkown system”，vim脚本文件发现该脚本文件与mac系统不兼容，
因此我选择采取第二方案：换用设备（搭载ubuntu系统）
   
---
###
按顺序执行以下指令
```
sudo apt install git 
ssh-keygen -t rsa -C "2690538311@qq.com"
cd  ~/.ssh
more id_rsa.pub
```
依次安装git；配置环境（创建密钥并拷贝至github中）
---
### 将代码克隆至本地
`git clone https://github.com/vesoft-inc/nebula`
### 安装依赖包
```
cd nebula
 ./build_dep.sh
 source ~/.bashrc
 mkdir build
```
### 创建build文件夹并进行cmake
```
cd build
cmake ..
make
sudo make install
```    
等待make的过程等待时间较长
### 进一步安装文件，完成nebula的配置
```
cd /usr/local/nebula
bash> cp etc/nebula-graphd.conf.default etc/nebula-graphd.conf
bash> cp etc/nebula-metad.conf.default etc/nebula-metad.conf
bash> cp etc/nebula-storaged.conf.default etc/nebula-storaged.conf
```
###
###

---
### 修改源代码以及编译
```
#include "base/Base.h"
#include <gtest/gtest.h>
#include "time/Duration.h"

using nebula::time::Duration;

TEST(Duration, elapsedInSeconds) {
    for (int i = 0; i < 5; i++) {
        Duration dur;
        auto start = std::chrono::steady_clock::now();
        sleep(2);
        auto diff = std::chrono::steady_clock::now() - start;
        dur.pause();

        ASSERT_EQ(std::chrono::duration_cast<std::chrono::seconds>(diff).count(),
                  dur.elapsedInSec()) << "Inaccuracy in iteration " << i;
    }
}

TEST(Duration, elapsedInMilliSeconds) {
    Duration dur;
    for (int i = 0; i < 200; i++) {
        dur.reset();
        auto start = std::chrono::steady_clock::now();
        usleep(5000);   // Sleep for 5 ms
        auto diff = std::chrono::steady_clock::now() - start;
        dur.pause();

        // Allow 1ms difference
        ASSERT_LE(std::chrono::duration_cast<std::chrono::milliseconds>(diff).count(),
                  dur.elapsedInMSec()) << "Inaccuracy in iteration " << i;
        ASSERT_GE(std::chrono::duration_cast<std::chrono::milliseconds>(diff).count() + 1,
                  dur.elapsedInMSec()) << "Inaccuracy in iteration " << i;
    }
}


int main(int argc, char** argv) {
    testing::InitGoogleTest(&argc, argv);
    folly::init(&argc, &argv, true);
    google::SetStderrLogging(google::INFO);

    return RUN_ALL_TESTS();
}
```    
### 修改源码后，在nebula/build/src/common/time/test路径下执行make操作，单独编译被修改的文件。
![image](https://github.com/johnson-623/johnson1/blob/master/images/a.jpg)

---
