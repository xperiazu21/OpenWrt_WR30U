# OpenWrt_WR30U
紀錄一下WR30U刷成官方OpenWrt的過程

## A. 獲取SSH

Source: [PatriciaLee3/wr30u_ssh](https://github.com/PatriciaLee3/wr30u_ssh)

### 準備:
1. Windows 電腦，需要有網路孔和其他上網方式(ex: Wi-Fi 或手機 USB 數據共享)

2. 安裝 Python 和 `pycryptodome` 3.17

3. 下載`server_emulator.py`

### 啟用 SSH Service

1. 路由器中設定以下部分:
   - 固定 WAN 至 Port1

   - 開啟 "启用与智能网关的无线配置同步"

   - 上網方式改為"DHCP"與"自動配置DNS"

2. 電腦中Wi-Fi網卡上右鍵開啟共用如圖

![image](https://github.com/xperiazu21/OpenWrt_WR30U/assets/53937642/f9ca75bc-2d34-4657-96fb-d844bae8d6f1)


3. 用網路線將路由器 Port1 和電腦連接，如果共用設定成功，路由器上網路指示燈會亮

4. 執行 `server_emulator.py` 並等待找到路由器連線

5. 找到後會顯示路由器資訊，按任意鍵繼續操作

6. 出現 finish 後即可關閉程式

7. 將網路線換回路由器上其他 LAN 口，即獲得臨時SSH權限。帳密為`root/admin`

## B. 備份原廠韌體分區

避免意外或是之後想還原，建議備份分區內容供日後還原

Source: [Github](https://github.com/openwrt/openwrt/pull/12770#issue-1732758292)

### 原廠韌體分區內容

下圖為 `cat /proc/mtd` 輸出:



其中只需要備份:

```
dev:    size   erasesize  name
mtd1: 00100000 00020000 "BL2"
mtd2: 00040000 00020000 "Nvram"
mtd3: 00040000 00020000 "Bdata"
mtd4: 00200000 00020000 "Factory"
mtd5: 00200000 00020000 "FIP"
mtd8: 02200000 00020000 "ubi"
mtd9: 02200000 00020000 "ubi1"
mtd12: 00040000 00020000 "KF"
```
