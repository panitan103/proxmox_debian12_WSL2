Installing Proxmox VE on WSL2
1. Install Debian 12 on WSL2

```sh
wsl --install -d Debian
```

2. enable systemd and disable generateHosts
```sh
sudo -i
nano /etc/wsl.conf

>> [boot]
systemd=true

[network]
generateHosts = false
```
nano /etc/hosts
>> 127.0.1.1       pve     pve.domain.local pvelocalhost

---------------------------

apt update && apt upgrade

apt install wget

echo "deb [arch=amd64] http://download.proxmox.com/debian/pve bookworm pve-no-subscription" > /etc/apt/sources.list.d/pve-install-repo.list
wget https://enterprise.proxmox.com/debian/proxmox-release-bookworm.gpg -O /etc/apt/trusted.gpg.d/proxmox-release-bookworm.gpg 
apt update && apt full-upgrade


---------------------

apt install proxmox-default-kernel
-------------------------

apt install proxmox-ve --no-install-recommends
