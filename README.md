# Passwall_For_iStoreOS
配置Passwall2至iStoreOS的试错与实践
---
## 1. 下载Passwall2适配版本-EasePi-R1
- 经过测试，适配的版本应该是`PassWall2_25.11.14_aarch64_generic_all_sdk_24.10.run`；
- 下载后，iStore→手动安装界面，上传下载的文件；
- 等待**安装成功**；
- 成功后，`Passwall2`将出现在“服务”选项卡中。

## 2. 设置自己的订阅
- 切换到`Node Subscribe`界面，拉到最底下，添加自己的飞机场；
- Shadowsocks 节点使用类型: `shadowsocks-libev`;
- Trojan 节点使用类型: `sing-box`;
- VMess 节点使用类型: `xray`;
- VLESS 节点使用类型: `xray`;
- Hysteria2 节点使用类型: `Hysteria2`;
- Sing-box 域名解析策略: `自动`;
- **点击: `保存并应用`**。

## 3. 配置Proxy（！重要！）
### Rule Manage下:
  #### 规则版本:
  - V2ray/Xray 资源文件目录: `/usr/share/v2ray/`
  - 自定义geoip文件更新链接: `https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geoip.dat`
  - 自定义geosite文件更新链接: `https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geosite.dat`
  - 开启 Geo 数据解析 + 手动更新 + 开启自动更新规则.
  #### Sing-Box/Xray 分流规则:
  - 新建Reject类(黑洞):
    - 域名: `geosite:category-ads-all`
   
  - 新建Steam_CN类(直连):           # 将游戏下载设置为直连
    - 域名: `geosite:steam@cn`
    - 域名: `domain:steamcontent.com`
    - 域名: `domain:steampipe.akamaized.net`

  - 新建Steam_Proxy类(规则):        # 将商店、社区设置为规则
    - 域名: `geosite:steam`

  - 新建Dierct类(中国大陆直连):
    - 域名: `xn--ngstr-lra8j.com`
    - 域名: `googleapis.cn`
    - 域名: `geosite:private`
    - 域名: `geosite:cn`
    - 域名: `geosite:category-games`

  - 新建Proxy类(规则):              # 通过代理转发流量
    - 域名: `geosite:geolocation-!cn`
  
### Node List下:
#### 添加新节点: `Xray 分流：分流总节点` :
  - 类型: `Xray`;
  - 协议名称: `分流`;
  - **以下按照顺序排列**:
    - Reject: `黑洞`;
    - Steam_CN: `直连`;
    - Steam_Proxy: `*你的节点*`;
    - Direct: `直连`;
    - Proxy: `默认`
    - 默认: `*你的节点*`
  - 域名解析策略: `Asls`;
  - 域名匹配算法: `hybrid`;
  - 点击 `**保存并应用**`

## 4. 回到 Basic Settings:
### 打开`**主开关**` `**路由器本机代理**` `**客户端代理**`
- 节点 Socks 监听端口: `1070`

---

## 大功告成：
### Steam商店秒开，下载地址直连：
```bash
] download_sources
Download sources:
- host st.dl.eccdnx.com, vhost st.dl.eccdnx.com, cell 0, CDN (#29), 1 connections of 1 max
- host dl.steam.clngaa.com, vhost dl.steam.clngaa.com, cell 0, CDN (#30), 1 connections of 1 max
- host xz.pphimalayanrt.com, vhost xz.pphimalayanrt.com, cell 0, CDN (#33), 0 connections of 1 max
Download jobs:
- type CDN, name st.dl.eccdnx.com, iteration 1, chunks: index 8171, 803 outstanding (60.48 MB), 3272 deferred, 4151 requested, 3348 succeeded, 0 failed. 76.8 Mbps 
- type CDN, name dl.steam.clngaa.com, iteration 1, chunks: index 9554, 921 outstanding (66.94 MB), 4848 deferred, 4706 requested, 3785 succeeded, 0 failed. 84.6 Mbps 
CAPIJobRequestUserStats - Server response failed 2

- 注：记得清理下载缓存并重启Steam；

### 以及其它……

---

只做个人经验记录笔记，仅供参考。
```
