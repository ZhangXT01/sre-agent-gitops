# sre-agent-gitops
#初始化
#配置网络
nmcli connection modify "ens160" ipv4.addresses 192.168.30.11/24 ipv4.gateway 192.168.30.2 ipv4.dns 192.168.30.2 ipv4.method manual connection.autoconnect yes
nmcli connection up "ens160"
hostnamectl set-hostname k8s-nodel

systemctl disable --now firewa1d
setenforce 0

#设置时区
timedatectl set-timezone Asia/Shanghai
#使用 dnf 安装 chrony
sudo dnf insta1l chrony
sudo systemctl start chronyd
sudo systemctl enable chronyd
#手动立即同步时间
sudo chronyc makestep
