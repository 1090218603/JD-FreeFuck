__如果您觉得这个项目不错的话可以在右上角给颗小星星吗？方便分享给更多的朋友吗？ (∩_∩)__

***

## 通知：
__2021/1/31__\
__由于某D安全团队介入，原作者Github项目资源被封或已下架，导致Linux直装失效，根据大佬给出的方案，经过本人的研究，现已推出基于GNU/Linux的[ Dokcer ](https://hub.docker.com/r/evinedeng/jd)版本，请大家重新部署，制作不易，有条件的朋友可以打赏，万分感谢！__

***

# 《JD薅羊毛》一键部署 For Linux
## 用途：通过JavaScript与Shell自动化脚本参与JD商城的各种活动从而白嫖J豆
## 支持的 Linux (简体中文) 发行版：
- __`Ubuntu`：支持 16.04 ~ 20.10 版本，建议优先使用Ubuntu系统__  　附：[Win10应用商店安装Ubuntu教程](https://github.com/SuperManito/JD-FreeFuck/wiki/Windows10-Install-Ubuntu)
- __`Debian`：支持 9.0 ~ 10.7 版本__
- __`Fedora`：支持 28 ~ 33 版本__
- __`CentOS`：支持 8.0 ~ 8.3 版本，如果是最小化安装，请通过SSH方式进入到终端__

  _温馨提示：尽量使用最新的稳定版系统，并且安装语言使用简体中文，旧版系统如果遇到问题请及时向我反馈，谢谢！_
    
***

# 下面进入正题，部署教程共三步，请认真阅读下面的内容
    
***

## 一、命令一键部署
- __Github：__

      bash <(curl -sL https://raw.githubusercontent.com/SuperManito/JD-FreeFuck/main/install.sh)
- __Gitee：__

      bash <(curl -sL https://gitee.com/SuperManito/JD-FreeFuck/raw/main/install.sh)
- 附1. 如果提示`Command 'curl' not found`则说明当前未安装`curl`软件包，安装命令如下：

      apt install -y curl 或 yum install -y curl
- 附2. 如果没有科学上网方式提示无法解决`Hosts`，可通过添加解析记录以解决连通性问题，添加命令如下：

      echo "199.232.96.133 raw.githubusercontent.com" >> /etc/hosts
      echo "151.101.88.133 raw.githubusercontent.com" >> /etc/hosts
- 附3. 如果执行一键命令后无效或部署后遇到报错怎么办？

      1）检查系统版本、联网状态等基本条件
      2）检查容器是否启动正常
      3）多次执行manual-update.sh更新脚本尝试
- 附4. 如果你已经安装了`Docker`不想用我的一键脚本？

      docker run -dit \
      -v /opt/jd/config:/jd/config `# 设置配置文件的主机挂载目录 /opt` \
      -v /opt/jd/log:/jd/log `# 设置日志的主机挂载目录 /opt` \
      -p 5678:5678 `# 设置端口映射，内部端口为5678，外部端口为5678` \
      -e ENABLE_HANGUP=true `# 启用挂机功能` \
      -e ENABLE_WEB_PANEL=true `# 启用控制面板功能` \
      --name jd `# 设置容器名为jd` \
      --network bridge `# 设置网络为桥接，直连主机` \
      --hostname jd `# 设置主机名为jd` \
      --restart always `# 设置开机自启` \
      evinedeng/jd:gitee
    
***

## 二、接下来我们需要您JD账户的“身份证”，它由`Cookie部分内容`组成，下面是获取途径：
__1. 在[ Wiki ](https://github.com/SuperManito/JD-FreeFuck/wiki/GetCookies)有详细的图文教程，请点击链接自行获取，此方式获取的Cookie有效期为1个月。__\
__2. 通过`控制面板`功能进入浏览器网页手机扫码获取，此方式获取的Cookie有效期为3个月。__

***

## 三、配置信息
### 将获得的`Cookie部分内容`填入下面命令中的“双引号”内，复制完整命令到终端并执行。（必填）
    sed -i '27c Cookie1=""' /opt/jd/config/config.sh
  _参考命令：sed -i '27c Cookie1="pt_pin=xxxxx;pt_key=xxxxxxx;"' /home/myid/jd/config/config.sh_
- 附1. 该项目可同时运行多个账号（最多6个），请按顺序填入下面命令中的“双引号”内，用几个就执行几条对应的命令，复制完整命令到终端并执行：

      sed -i "28c Cookie2=$COOKIE2" /opt/jd/config/config.sh
      sed -i "29c Cookie3=$COOKIE3" /opt/jd/config/config.sh
      sed -i "30c Cookie4=$COOKIE4" /opt/jd/config/config.sh
      sed -i "31c Cookie5=$COOKIE5" /opt/jd/config/config.sh
      sed -i "32c Cookie6=$COOKIE6" /opt/jd/config/config.sh
- 附2. 如果需要使用[ Server酱 ](http://sc.ftqq.com/)微信推送功能请将`SCKEY`填入下面的双引号内，复制完整命令到终端并执行：

      sed -i '70c export PUSH_KEY=""' /opt/jd/config/config.sh

***

## 四、使用与更新
- 1.如何运行脚本开始白嫖京豆？

      bash run-all.sh
- 2.如何更新活动脚本？

      bash manual-update.sh
    _注：建议每次运行活动脚本前执行一次，JD活动经常变化，原作者更新也很频繁。_
- 3.如何查看帮助文档并获取更多功能？

      docker exec -it jd cat readme.md
- 4.如何更新一键脚本？

      bash <(curl -sL https://raw.githubusercontent.com/SuperManito/JD-FreeFuck/main/update.sh)
    _注：适用于后期维护更新，当先前一键脚本失效需要更新时会在项目置顶通知。_
    
***

## 五、声明
1. 本人项目为二次使用，我不是该《JD薅羊毛》项目的开发者，所有活动类问题与我无关。
2. `run-all.sh`为本人编写的一键执行所有活动脚本，`manual-update.sh`为本人编写的一键更新脚本，自己查看一下这两个文件内容就全明白了，如果你不想用我写的一键脚本请自行删除，其余所有文件均为原作者创作。
    
***

## 六、项目需知
1. 该项目配置文件以及一键脚本所在目录为/opt/jd
2. 此项目涉及 docker 容器技术，如果你对 docker基础命令 一无所知，那么请不要随意改动容器
3. 执行脚本期间可能会卡住或运行挂机脚本，可通过命令 Ctrl + ZC 跳过继续执行剩余活动脚本
4. 由于JD活动一直变化所以会出现无法参加活动、报错等正常现象，可手动更新活动脚本
5. 如果需要更新活动脚本，请执行 bash manual-update.sh 命令进行一键更新即可
6. 之前填入的 Cookie 部分内容具有一定的时效性，若提示失效请根据教程重新获取并通过命令手动更新
7. 如果需要查看帮助文档以及获取更多功能，请通过 docker exec -it jd cat readme.md 命令进行查看
8. 因为本人每天也在使用，遇到错误会在第一时间解决，遇到任何与部署相关的问题都可访问本项目寻求帮助

***

## 如果您有意见与建议欢迎到 [Issuse](https://github.com/SuperManito/JD-FreeFuck/issues) 反馈
## 如果老板成功薅到羊毛，赏1元可否(∩_∩)
<img src="https://a1.qpic.cn/psc?/V50n9XtX0l0n6J3udmyK2gRcEx1lPmFH/ruAMsa53pVQWN7FLK88i5m6GsPj*rJQrKSo6N9UFZGC1BHFpPrrRaDcpZz.ySsybH7kPVI1SDrOmO1SVGbzEgP*3kd0m0SctQXeeBRZE3iA!/b&ek=1&kp=1&pt=0&bo=6QTpBOkE6QQDEDU!&tl=1&vuin=1808077397&tm=1611579600&sce=60-1-1&rf=viewer_311" width="330" height="330" alt="微信赞赏码"/><br/>
