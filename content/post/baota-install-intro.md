+++
title = '寶塔安裝筆記與繞過套件付費機制'
date = 2024-04-25T23:11:56+08:00
draft = false
+++

# 寶塔安裝筆記

> 破解版本屬於非正規，此文件僅供自己筆記與教學性質，請勿使用於商業環境。
> 參閱官方 Github https://github.com/aaPanel/BaoTa

### 寶塔介紹
寶塔是很好用的伺服器維運面板，提供友善的介面與圖表，多元的套件商店，甚至有支援手機APP。在快速建置伺服器或是對於伺服器配置不熟悉，裝上寶塔後，都可以快速使用UI，對於快速需要建置商案或是小應用非常方便。

### 前言
破解版本目前僅能使用 `v7.7.0` 版本以前，之後版本都會驗證 `userinfo.json`。

### 安裝寶塔

1. 安裝 `v7.7.0` 版本腳本，原作者 Github (https://github.com/8838/btpanel-v7.7.0)
```
curl -sSO https://raw.githubusercontent.com/8838/btpanel-v7.7.0/main/install/install_panel.sh && bash install_panel.sh
```

2. 移除手機號碼阻擋
```
sed -i "s|bind_user == 'True'|bind_user == 'XXXX'|" /www/server/panel/BTPanel/static/js/index.js
```

3. 刪除強制綁定手機js文件
```
rm -f /www/server/panel/data/bind.pl
```

快速一鍵優化腳本
```
wget -O optimize.sh http://f.cccyun.cc/bt/optimize.sh && bash optimize.sh
```

擔心未來站點被移除，以下為備份腳本。
* [optimize.sh](/files/optimize.sh)

### 寶塔套件開心版
> 寶塔各種套件是需要收費的，以下為繞過付費機制的方式。僅供教學使用

1. 手動將付費套件改為永不過期
```
文件路徑 `/www/server/panel/data/plugin.json`
搜尋 `"endtime": -1` 全部替換為 `"endtime": 999999999999`
```

2. 調整 `plugin.json` 權限，防止被改回免費版本
```
chattr +i /www/server/panel/data/plugin.json
```

快速一鍵腳本
```
curl -sSO https://raw.githubusercontent.com/ztkink/bthappy/main/one_key_happy.sh && bash one_key_happy.sh
```

擔心未來站點被移除，以下為備份腳本。
* [one_key_happy.sh](/files/one_key_happy.sh)


### 寶塔降版本

> 也許有時候誤觸面板上的升級或修復按鈕，導致版本升級無法繼續使用開心版本。

1. 下載 `v7.7.0` 版本
```
wget https://d.ybfl.xyz/bt/LinuxPanel-7.7.0.zip
```

2. 解壓縮
```
unzip LinuxPanel-7.7.0.zip
```
> 如果有提示輸入大寫A，全部替換

3. 進入升級目錄
```
cd /root/panel
```

4. 執行降級
```
bash update.sh
```


### 相關筆記連結(多半來源為中國)

[403 Forbidden解決方案](https://www.wdzzz.com/yunying/idc/2471.html)
[鍵站無域名解決方案](https://blog.csdn.net/dccose/article/details/127012649)
[如何查看寶塔面板地址](https://www.bt.cn/bbs/thread-33886-1-1.html)