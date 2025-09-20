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
