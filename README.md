# Create password for root
sudo passwd;
# Change user to root
su;
# Under root made update and install
apt-get update;
apt-get -y install tmux git kali-root-login;

# Reboot and login as root
cd /tmp;
git clone https://github.com/Bearsec/tmux.conf;
cp /tmp/tmux.conf/.tmux.conf /root/;
rm -rf /tmp/tmux.conf;
git clone https://github.com/Bearsec/new-kali-setup;
cd /tmp/new-kali-setup;
cp ./mount-shared-folders /usr/local/sbin/mount-shared-folders;
chmod +x /usr/local/sbin/mount-shared-folders;
cp ./restart-vm-tools /usr/local/sbin/restart-vm-tools;
chmod +x /usr/local/sbin/restart-vm-tools;
cd ..;
rm -rf /tmp/new-kali-setup;
ln -s /usr/local/sbin/mount-shared-folders /root/Desktop/mount-shared-folders;
ln -s /usr/local/sbin/restart-vm-tools /root/Desktop/restart-vm-tools;
echo "set vb" >> ~/.vimrc;
echo "xset b off" >> ~/.xession;
xset b off;
echo "set bell-style none" >> /etc/inputrc;
echo "blacklist pcspkr" >> /etc/modprobe.d/blacklist.conf;
touch ~/.hushlogin;
# Create VPN ip monitor
echo "#!/bin/bash" >> /usr/local/sbin/vpn-ip-mon
echo "if ifconfig tun0 | grep -q 'inet'; then echo `/sbin/ip -o -4 addr list tun0 | awk '{print $4}' | cut -d/ -f1`; else echo 'NO VPN'; fi" >> /usr/local/sbin/vpn-ip-mon
chmod +x /usr/local/sbin/vpn-ip-mon
# Create xfce gen-mon 
sh -c "/usr/local/sbin/vpn-ip-mon" 2>/dev/null
