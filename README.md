# EeePC701InstallAlpine
17年前的Eee PC 701仍能安裝最新的係業系統並能使用AI你信嗎?

首先到官網下載Alpine x86 鏡像:
https://alpinelinux.org/downloads/

下戴Rufus將鏡像寫入USB Disk:
https://rufus.ie/en/

以USB盤啟動電腦, 然後先執行以下指令以減少安裝系統預設使用的容量空間:
```
export BOOT_SIZE=100
export SWAP_SIZE=0
export ROOTFS=ext2
```
然後執行以下安裝Alpine Linux的腳本:
```
setup-alpine
```
安裝過程可參考以下Wiki資料:
https://wiki.alpinelinux.org/wiki/Alpine_setup_scripts

完成安裝後先關閉電腦
```
poweroff
```
駁出USB Disk後以硬碟啟動Alpine Linux,
登入後進入CLI環境, 執行以下指令更新套件庫:
```
apk update
```
再來安裝以下套件:
```
apk add nano curl jq
```
然後便可創建Gemini腳本:
```
nano ask.sh
```
腳本中輸入以下內容:
```
#!/bin/sh
# 設定 API base URL（將API_URL替換為存取Gemini服務的API URL）
API_BASE="API_URL"

# 設定 Gemini API 金鑰（替換為你的API KEY）
API_KEY="API_KEY"

# 使用的模型（可選 gemini-2.5-flash 或其他）
MODEL="gemini-2.5-flash

# 取得使用者輸入的問題
QUESTION="$1"

# 發送請求
curl -s "$API_BASE" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $API_KEY" \
  -d '{
    "model": "'"$MODEL"'",
    "messages": [{"role": "user", "content": "'"$QUESTION"'"}],
    "temperature": 0.7
  }' | jq -r '.choices[0].message.content'
```
按Ctrl+x, 再按y保存, Enter退出後
為腳本加上執行權限:
```
chmod +x ask.sh
```
然後便可用以下方式向Gemini發問:
```
./ask.sh "Ask your question"
```
