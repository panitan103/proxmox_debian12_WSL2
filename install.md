Installing Proxmox VE on WSL2
1. Install Debian 12 on WSL2

```sh
wsl --install -d Debian
```

2. enable systemd and disable generateHost

```sh
sudo -i
nano /etc/wsl.conf
```
```sh
[boot]
systemd=true

[network]
generateHosts = false
```

3. remove 127.0.1.1 in /etc/hosts
```sh
nano /etc/hosts
```
```sh
# [network]
# generateHosts = false
127.0.0.1       localhost
#127.0.1.1      #remove/comment this line

192.168.1.16    host.docker.internal
192.168.1.16    gateway.docker.internal
127.0.0.1       kubernetes.docker.internal

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
Run hostname --ip-address to check your ip address
```sh
hostname --ip-address
# output should return all of your IP address from host
```
Reboot once after edit
```sh
wsl --shutdown
wsl -d Debian
```
---------------------------

4. Install Proxmox VE https://pve.proxmox.com/wiki/Install_Proxmox_VE_on_Debian_12_Bookworm

add Proxmox VE Repository and update 

```sh
apt update && apt upgrade -y && apt install wget -y

echo "deb [arch=amd64] http://download.proxmox.com/debian/pve bookworm pve-no-subscription" > /etc/apt/sources.list.d/pve-install-repo.list
wget https://enterprise.proxmox.com/debian/proxmox-release-bookworm.gpg -O /etc/apt/trusted.gpg.d/proxmox-release-bookworm.gpg 

apt update && apt full-upgrade
```

Then install proxmox kernel

```sh
apt install proxmox-default-kernel
```
Reboot once after install proxmox kernel
```sh
wsl --shutdown
wsl -d Debian
```

insatll proxmox-ve
```sh
apt install proxmox-ve --no-install-recommends
```
