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

 
TEST(WallClock , time1 ) {

    std::vector<int64_t> timer;
    std::vector<int64_t>s;

    for (uint32_t i = 0; i < 10; i++) {

        auto sec=WallClock::slowNowInMicroSec();
        usleep(3000);
        auto sec2=WallClock::slowNowInMicroSec();
        auto cost_time=sec2-sec;
        timer.push_back(cost_time);
    }
    std::cout << timer[0] << std::endl;
    int64_t sum=std::accumulate(timer.begin(),timer.end(),0);
    double average=sum*1.0/10;
    std::cout << "Mean Error  : " << average-3000 << "ms "<<std::endl;

    for(int i = 0; i < 10 ; i++ ){
        int64_t a=(timer[i]-average)*(timer[i]-average);
        s.push_back(a);
    }

    int64_t sum2=std::accumulate(s.begin(),s.end(),0);
    double variance=sum2*1.0/9;
    std::cout << "The  Variance  Is : "<< variance << std::endl;
    double error=( abs(average-3000) * 1.0 / 3000) * 100;
    std :: cout << "Test Error Is  : " << error  << "%" << std::endl;

}


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
---  
### 修改源码后，在nebula/build/src/common/time/test路径下执行make操作，单独编译被修改的文件。
![image](https://github.com/johnson-623/johnson1/blob/master/images/a.jpg)
---
该程序用于测试延迟，usleep()函数的延迟误差利用fastNowInMicroSec()函数进行计算，同时计算出了时间误差的均值。可以得出结论：slowNowInMicroSec()在速度较慢的同时具有更高的精确程度。 
![image](https://github.com/johnson-623/johnson1/blob/master/images/b.jpg)
---
通过 `git config --global user.name"johnson-623"` 以及 `git config --global user.email"2690538311@qq.com" `绑定自己的github账号以及邮箱
### 依次执行以下指令：
```
git status//检查文件是否存在改动
git add//加入上传文件到缓存
git commit//将缓存区内容添加到本地仓库中
git push//将改动后的文件上传到自己的GitHub仓库中
git remote//查看自己设置的所有名字
```
![image](https://github.com/johnson-623/johnson1/blob/master/images/d.jpg)
`git branch change`
`git checkout change`

### git push时遇到报错：
```
mac@macdeMBP test % git push --set-upstream origin change
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
mac@macdeMBP test % git push --set-upstream origin change
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.
```
**解决方案：重新生成密钥**

`fatal: The current branch change has no upstream branch.`

![image](https://github.com/johnson-623/johnson1/blob/master/images/c.jpg)
**解决方案：先输入git pull命令后重试git push**

---
### 选择已修改的分支，提交Pull Request，提交成功
![image](https://github.com/johnson-623/johnson1/blob/master/images/g.jpg)
---
## 总结与心得
非常感谢吴老师以及本学期的C++课程，能够让我在大二阶段就接触到了开源项目。虽然在完成的大作业的过程中存在着非常大的挑战，但是收获却是难以言喻的。例如命令行的使用，git hub的了解以及Markdown语法的逐步熟悉，都为我提供了大于同龄人本专业同学更广阔视野得机会。最后的一堂课后，老师悉心为我们指导，虽然这辆“车”不好修，但是在老师的悉心指导和帮助（老师太敬业了！！！指导我们到下午两点多）下顺利地解决了环境搭建或是工程操作过程中所遇到一些困难。老师的授课风格是我目前为止见过最有个性的，我相信挑战和难度是促进我们快速进步的原动力，而相比起安逸而碌碌无为地度过大学四年我更偏向选择前者。C++ primer也是我大学阶段到目前为止所见过的最厚实的一本教材，它以C语言为基础但却有更为深奥，想要更加牢固地掌握它还需要我在课后的不断巩固和编程实践。仍然记得老师教导我们使用github和豪言谈论近来来热门的言语，在这个过程中我也学会了如何向老师的项目上用PR的方式提出自己的想法和见解。或许，对于五年后的我来说，理解本次单元测试的代码并不具有很大的困难，但是这门课程所带给我的，却远远不是这一小段代码这么简单的！

**持续更新中** 2019.12.26


