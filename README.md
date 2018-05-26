# ArchiSteamFarm
### Install Debian/Ubuntu
```shell
sudo apt-get update
sudo apt-get install wget unzip screen libunwind8 liblttng-ust0 libcurl3 libssl1.0.0 libuuid1 libkrb5-3 zlib1g libicu52 -y //Ubuntu 14.x
sudo apt-get install wget unzip screen libunwind8 liblttng-ust0 libcurl3 libssl1.0.0 libuuid1 libkrb5-3 zlib1g libicu55 -y //Ubuntu 16.x
sudo apt-get install wget unzip screen libunwind8 liblttng-ust0 libcurl3 libssl1.0.0 libuuid1 libkrb5-3 zlib1g libicu57 -y //Ubuntu 17.x
mkdir ASF && cd ASF
sudo wget $(curl -s https://api.github.com/repos/JustArchi/ArchiSteamFarm/releases/latest | grep browser_download_url | grep 'linux-x64[.]zip' | head -n 1 | cut -d '"' -f 4) && unzip ASF-linux-x64.zip && rm ASF-linux-x64.zip && sudo chmod +x ArchiSteamFarm
```
GroupID64查询方法:
点开你的组的页面，地址栏会是这样子：  
https://steamcommunity.com/groups/thesharing  
然后在地址后面加上/memberslistxml/?xml=1，这时候地址栏是这样子的：  
https://steamcommunity.com/groups/thesharing/memberslistxml/?xml=1  
SteamID64： 查询地址https://steamrepcn.com/
```shell
vim config/xxx.json
{
        "Enabled": true,
        "SteamLogin": "自己的steam登录用户名",
        "SteamPassword": "自己的steam登录密码",
        "FarmOffline": false,
        "ShutdownOnFarmingFinished": true,
        "CardDropsRestricted": true,
        "ShutdownOnFarmingFinished": false,
        "SteamMasterClanID": 建立的组GroupID64,
        "CurrentCulture": "zh-CN",
        "SteamUserPermissions": {
            "自己的SteamID64": 3
        },
        "DismissInventoryNotifications": false
}
```
一些参数解释
```
Debug                     //默认值为false，True调试模式，不建议开启
FarmOffline               //默认值为false，True挂卡时不显示游戏状态
ShutdownOnFarmingFinished //True挂完卡自动退出
```
vim config/ASF.json将"CurrentCulture"的值改为"zh-CN"

直接运行./ArchiSteamFarm

以screen运行
```
screen -S ASF        //新建一个名为ASF的窗口  
./ArchiSteamFarm  
```
按 ctrl +a +d 进入后台
```
screen -ls              //列出当前所有的窗口  
    Detached---->挂起状态，无终端在连接会话    
    Attached---->有终端在连接会话    
   
screen -r ASF           //恢复窗口  
screen -S ASF -X quit   //删除窗口  
```


在组聊天窗口可以输入命令
```
!play AppID               //切换成手动挂卡，单独挂指定游戏的AppID
!resume                   //切换回自动挂卡
!addlicense AppID或SubID  //用于添加免费或限时免费的游戏
!r AAAAA-BBBBB-CCCCC      //尝试激活key，注意VPS的地区
!iqadd AppID              //新增指定AppID优先挂卡
!iqrm AppID               //从优先挂卡队列删除指定的AppID
!iq                       //显示优先挂卡的队列
!unpack                   //将库存内的补充包全部拆开
!badd AppID               //把游戏加进黑名单
```

---

## Description

ASF is a C# application that allows you to farm steam cards using multiple steam accounts simultaneously. Unlike Idle Master which works only for one account at given time, requires steam client running in background, and launches additional processes imitating "game playing" status, ASF doesn't require any steam client running in the background, doesn't launch any additional processes and is made to handle unlimited steam accounts at once. In addition to that, it's meant to be run on servers or other desktop-less machines, and features full cross-OS support, which makes it possible to launch on any .NET Core-supported operating system, such as Windows, Linux or OS X. ASF is possible thanks to gigantic amount of work done in marvelous **[SteamKit2](https://github.com/SteamRE/SteamKit)** library.

ASF doesn't require and doesn't interfere in any way with Steam client. In addition to that, it doesn't require exclusive access to given account, which means that you can use your main account in Steam client, and use ASF for idling the same account at the same time. If you decide to launch a game, ASF will get disconnected, and resume idling once you finish playing your game, being as transparent as possible during entire process.

---

### Core features

- Automatic idling of available games with card drops using any number of active accounts
- No requirement of running or even having official Steam client installed
- Guarantee of being VAC-free
- Complex error-reporting mechanism, allowing ASF to be smart and resume idling even in case of Steam or networking problems
- Customizable cards idling algorithm which will push performance of card drops to the maximum
- Offline idling, allowing you to skip in-game status and stop confusing your friends
- Advanced support for alt accounts, including ability to redeem keys, redeem gifts, accept trades and more through a simple Steam chat
- Support for latest Steam security features, including SteamGuard, SteamParental and two-factor authentication
- Unique ASF 2FA mechanism allowing ASF to act as a mobile authenticator (if needed)
- StreamTradeMatcher integration allowing ASF to help you in completing your steam badges by accepting dupe trades
- Rebased on .NET Core 2.0, cross-OS compatibility, official support for Windows, Linux and OS X
- ...and many more!

---

### Setting up / Help

Detailed guide regarding setting up and using ASF is available on our wiki in **[setting up](https://github.com/JustArchi/ArchiSteamFarm/wiki/Setting-up)** section.

---

### Compatibility / Supported operating systems

ASF officially supports Windows, Linux and OS X operating systems. Please visit **[compatibility](https://github.com/JustArchi/ArchiSteamFarm/wiki/Compatibility)** section on the wiki for more info.

---

### Want to know more?

Our **[wiki](https://github.com/JustArchi/ArchiSteamFarm/wiki)** includes a lot of other articles that might help you further with using ASF, as well as show you everything that you can make use of.
