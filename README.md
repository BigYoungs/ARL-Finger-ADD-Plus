# ARL-Finger-ADD-Plus

## 主要功能

批量添加ARL指纹，支持：`ARL V2.6及以前版本`。

ARL最近更新了V2.6.1版本，重大变更：更新指纹检测规则。

**如你使用的ARL V2.6.1版本以后的新版本，请移步新版本导入工具：[ARL-Finger-ADD-Pro](https://github.com/BigYoungs/ARL-Finger-ADD-Pro)**

> 提示：ARL-Finger-ADD-Pro和ARL-Finger-ADD-Plus，两个工具不通用，请根据自己使用版本，谨慎选择使用工具。

## 已支持导入的指纹库列表，共计：9001个

1. [Ehole3.1](https://github.com/EdgeSecurityTeam/EHole/releases/tag/v3.1)自带的指纹文件，Finger有1007个

2. [Finger](https://github.com/EASY233/Finger/blob/main/library/finger.json) 截止2023年3月11日最新版，Finger有1007个

3. [FingerprintHub](https://github.com/0x727/FingerprintHub/blob/main/web_fingerprint_v3.json) 截止2023年11月23日最新版，Finger有2839个

4. dismap 截止2023年12月17日最新版，Finger有4598个


## 用法:

```
提示：本工具只适配此项目源码下的Finger指纹，网上下载的Finger指纹可能不适配，如需使用网上下载的Finger指纹，需要自行修改代码。

Usage: ARL_Finger_Add_Plus.py [options]

Options:
  -h, --help                  show this help message and exit
  -u URL, --url=URL           Please Enter the ARL Site Url
  -a AUTH, --auth=AUTH        Please Enter Your ARL username password
  -f FINGER, --finger=FINGER  Please Enter You Want import Finger, eg:
                              1：Ehole3.1_finger.json        2：Finger_finger.json
                              3：FingerprintHub_finger.json  4：Dismap_rule.go
                              all: 导入工具支持的所有指纹
  -t TOKEN, --token=TOKEN     Please Enter Your ARL Auth Token

使用示例：

ARL API Key 用法：
python3 ARL_Finger_ADD_Plus.py -u http://192.168.1.1:8888 -t 1234567890abcdefg -f all

ARL 用户名密码 用法：
python3 ARL_Finger_ADD_Plus.py -u http://192.168.1.1:8888 -a admin:arlpass -f all

```

## 版本记录

### v1.0.0 2023-11-23

> 提示：此版本参考Github上[ARL-Finger-ADD](https://github.com/loecho-sec/ARL-Finger-ADD)的代码，感谢原作者

1. 修复Bug：资产有多个指纹规则的，添加为多个指纹规则，而不是一个指纹规则

> 比如："keyword": ["WSY_logo","管理系统 MANAGEMENT SYSTEM"]
>
> 源代码添加的规则是：body="WSY_logo"，优化后添加的规则是：body="WSY_logo" || body="管理系统 MANAGEMENT SYSTEM"，下文截图有体现

2. 修复Bug：源代码添加源指纹库时，不添加header规则，优化后添加header规则，如：header="ecology_JSessionid"

3. 优化认证方式，支持ARL原生的ARL API KEY认证模式，也支持ARL的用户名密码认证模式，两个参数都配置，优先使用ARL API KEY认证模式

> ARL API KEY配置教程：https://tophanttechnology.github.io/ARL-doc/api/

4. 更换默认finger.json文件，使用[Ehole3.1](https://github.com/EdgeSecurityTeam/EHole/releases/tag/v3.1)
   自带的指纹库，3.0指纹库只有683个，3.1增加到998个

5. 修改了指纹上传接口，使用ARL的upload接口，因为upload接口支持去重（去重规则暂未了解）

6. 优化代码逻辑（大家无需关心）

### v1.1.0 2023-11-26
支持导入Finger指纹，已完成

### v1.2.0 2023-11-27

> 提示：此版本已经重构代码，完全不同于v1.0.0版本，但仍然感谢原作者给我带来的灵感

支持导入FingerprintHub指纹，已完成

### v1.3.0 2023-12-17
支持导入Dismap指纹，共计4598个
> 提示:
> Dismap的指纹库，需要使用此项目里的all_fingers/dismap_rule.go文件，不要使用网上下载的dismap项目rule.go文件，因为网上下载的dismap_rule.go文件，不适配此项目的代码。如果实在要换，照着我的格式改一下。

### V1.3.1 2023-12-25

修复使用-a admin:arlpass 认证模式时，报401：未登录的报错


**重要：** 导入Dismap指纹库，需要先修改ARL的Nginx配置，否则会提示413错误，具体修改方法如下：
```
# 以下内容针对ARL容器部署的情况，如果是源码部署的，同理

1. 进入到arl-web容器里，执行：docker exec -it arl-web /bin/bash

2. vim /etc/nginx/nginx.conf

3. 在http块下，添加以下内容：
    client_max_body_size 20m;

4. 重启nginx：nginx -s reload

5. 退出容器：exit

6. 重新运行脚本，或者直接通过ARL的web界面导入指纹库：tmp_finger.json
```


## TODO

计划增加以下指纹库支持：

- [x] [Finger](https://github.com/EASY233/Finger/blob/main/library/finger.json) 截止2023年3月11日最新版，Finger有1007个
- [x] [dismap](https://github.com/zhzyker/dismap/blob/main/readme-zh.md#-rulelab) 截止2023年11月23日最新版，Finger有4598个
- [x] [FingerprintHub](https://github.com/0x727/FingerprintHub/blob/main/web_fingerprint_v3.json)   截止2023年11月23日最新版，Finger有2839个

## 添加后的效果

**指纹规则支持逻辑或`||`，如下图所示**

![image](4.png)

## 版权声明

ARL-Finger-ADD-Plus本软件，通过BigYoung购买专栏后，有权进行个人使用，禁止公开发布和用于商业用途，否则BigYoung有权追究法律责任。

## 免责声明

ARL-Finger-ADD-Plus 仅供学习交流使用，禁止用于非法用途，否则后果自负。

## 下载地址&获取最新版

[https://afdian.net/a/bigyoung?tab=shop](https://afdian.net/a/bigyoung?tab=shop)
