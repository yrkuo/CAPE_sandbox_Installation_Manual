# CAPE_sandbox_Installation_Manual
Record how to install CAPE Sandbox

## 基本環境
```
* Host OS: Ubuntu 22.04 LST(recommend)
* Guest OS: Windows 10 x64 2004
* CAPE: V2
* Virtualization software: KVM
* Python Version: 3.10.6
```

## 前置作業

* 在 host 端創建名為 cape 的使用者 => `adduser cape`
* 給予 cape 使用者 sudo 權限 => `sudo usermod -aG sudo cape`  
NOTE: 底下所有安裝過程皆以cape使用者身分進行


## Install CAPE

1. 下載自動化安裝腳本 => [cape2.sh](https://github.com/kevoreilly/CAPEv2/blob/master/installer/cape2.sh)  
2. 修改腳本執行權限 => `chmod a+x cape2.sh`
3. 安裝CAPE => `sudo ./cape2.sh all cape | tee cape.log`
4. 重新開機

## Install KVM

1. 下載自動化安裝腳本 => [kvm-qemu.sh](https://github.com/doomedraven/Tools/blob/master/Virtualization/kvm-qemu.sh)  
2. 將腳本中的 `<WOOT>` 更改為任意 4 chars，e.g. 0A08
3. 安裝 KVM => `sudo ./kvm-qemu.sh all cape | tee kvm-qemu.log`
4. 重新開機
3. 安裝 Virtual Machine Manager => `sudo ./kvm-qemu.sh virtmanager cape | tee kvm-qemu-virt-manager.log`
4. 重新開機

## Install CAPE’s dependencies

1. 變更路徑 => `cd /opt/CAPEv2/`
2. 安裝相依性套件 => `sudo poetry install`
3. 修改套件版本 => `sudo -u cape poetry run pip3 install pyOpenSSL==22.0.0`


## Guest配置

創建一虛擬機器，作業系統為win10。
* 參考連結[how-to-create-virtual-machine-with-virt](https://www.doomedraven.com/2020/04/how-to-create-virtual-machine-with-virt.html)
* 一些基礎的 anti-vm 設定可參考[Modifying KVM (qemu-kvm) settings for malware analysis](https://www.doomedraven.com/2016/05/kvm.html#modifying-kvm-qemu-kvm-settings-for-malware-analysis)
* 修改 guest 端的network configuration => [network configuration](https://capev2.readthedocs.io/en/latest/installation/guest/network.html)
IMPORTANTT!!! 網路設置為hostonly的情況下，guest是沒有連外網的能力的
* 在 guest 端放置 agent.py => [installing the Agent](https://capev2.readthedocs.io/en/latest/installation/guest/agent.html)
* 額外配置 => [additional configuration](https://capev2.readthedocs.io/en/latest/installation/guest/additional_configuration.html)


## 執行CAPE

1. 變更路徑 => `cd /opt/CAPEv2/`
2. 執行CAPE => `sudo -u cape poetry run python3 cuckoo.py`
3. 提交欲分析的檔案 => `sudo -u cape poetry run python3 ./utils/submit.py /path/to/file`








