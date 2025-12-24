# Proxmox VE ( P.VE ) Installation Commands
- Update your system's package list and perform a full upgrade:
```apt update && apt full-upgrade -y```
- Verify your hostname resolves to a non-loopback IP address.
```hostname --ip-address```
- Now the IP the last command gives, use that in:
```nano /etc/hosts```
- In /etc/hosts, paste this. ( Note - Edit {your ipv4} to your vps ip )
``127.0.0.1 localhost
( your ipv4 ) proxmox.yourdomain.com proxmox``
! Note, don't clear whole file, clear the first 2 files then paste this. In one word don't delete ipv6 type in /etc/hosts ~
- Add the Proxmox VE repository.
```echo "deb [arch=amd64] http://download.proxmox.com/debian/pve bookworm pve-no-subscription" > /etc/apt/sources.list.d/pve-install-repo.list```
- Add the Proxmox VE repository key.
```wget https://enterprise.proxmox.com/debian/proxmox-release-bookworm.gpg -O /etc/apt/trusted.gpg.d/proxmox-release-bookworm.gpg```
- Update your repository and system again with the new source.
```apt update && apt full-upgrade -y```
- Install the Proxmox VE kernel and reboot.
```apt install proxmox-default-kernel -y```
```reboot```
~ After the system reboots, reconnect via SSH and install the Proxmox VE packages.
- Reconnect to VPS after reboot, and install Proxmox Virtual Environment.
```apt install proxmox-ve postfix open-iscsi chrony -y```
( During this step, you may be prompted to configure postfix; choose the "local only". )
- Remove the default Debian kernel to prevent potential conflicts during future upgrades.
```apt remove linux-image-amd64 'linux-image-6.1*' -y```
```update-grub```
- (Optional) Remove the os-prober package if you are not dual-booting.
```apt remove os-prober -y```
- Reboot the VPS one last time to boot into the Proxmox VE kernel.
```reboot```
