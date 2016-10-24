How to set up a virtual web development environment
===================================================

Preliminaries
-------------
This guide will get you started with setting up a virtual web development environment on Linux or Windows with English language and Norwegian setup.

The guide will use the following software.
* Ubuntu / Windows Host
* Ubuntu 16.10 Guest
* Oracle Virtualbox

## 1. Installing Virtualbox ##

1. Download virtualbox from: http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html
2. Install Virtualbox

## 2. Setting up a new VM ##

* Name: <code>host</code>-vm-<code>name</code>
* RAM: <code>4096 MB</code> or greater.
* Dynamic disk: <code>60 GB</code> or greater.

After the vm is created, enter settings and select network type <code>Bridged</code>.

## 3. Download and install Ubuntu Server 16.10 ##

1. Download Ubuntu Server 16.10 from here: https://www.ubuntu.com/download/server
2. Mount the downloaded iso image as a CD-rom for your Virtual Machine.
3. Start the VM.
4. Initialize the setup:
	1. Choose: <code>Enhlish</code>
	2. Choose: <code>Install Ubuntu Server</code>
	3. Choose: <code>English</code>
	4. Choose: <code>other</code>
	5. Choose: <code>Europe</code>
	6. Choose: <code>Norway</code> (yes, you can press n to jomp down the list)
	7. Choose: <code>United States</code>
5. Configure the keyboard
	1. Detect keyboard layout: <code>Yes</code>
	2. Press keys asked for.
	3. You do have a key labeled <code>'2 ²'</code>, select <code>No</code>
	4. You do not have a key with <code>'ö'</code>, select <code>No</code>
	5. You do not have a key with <code>'é'</code>, select <code>No</code>
	6. You do not have a key with <code>'ç'</code>, select <code>No</code>
	7. You do have a key with <code>'æ'</code>, select <code>Yes</code>, press <kbd>æ</kbd>
	8. "no" should have been detected, select Yes if so, or try again to detect.
	9. Wait. Loading, less than 1 min.
6. Configuring
	1. Choose hostname: <code>host</code>-vm-<code>name</code>
	2. Write in your full name
	3. Select a username.
	4. Select a password.
	5. Confirm password.
	6. Encrypt home directory: <code>No</code>
	7. <code>Europe/Oslo</code> should have been selected for timezone, select <code>Yes</code> if so.
7. Setting up disks
	1. Select <code>Guided</code> - <code>use entire disk and set up LVM</code>
	2. Select the selected disk
	3. Select <code>Yes</code> to write the changes to disk.
	4. Choose the preselected value for disk size.
	5. Select <code>Yes</code> to write the changes to disk.
	6. Wait. System now installing, should take about 1-2 mins.
8. Configuring
	1. Select <code>no proxy</code>.
	2. Wait. Packages is fetched and updates are running, should take less than 1 min.
	3. <code>Install security updates automatically</code>.
	4. Select only package: <code>standard system utilities</code>.
	5. Wait. Installing, about 1 min.
	6. Install grub: <code>Yes</code>
	7. Wait. Finishing: less than 1 min.
	8. Virtual cd should be removed automatically, select <code>continue</code> to reboot.
9. Finalizing
	1. Wait for the vm to reboot.
	2. Log in to the vm.
	3. Run:
```
sudo apt-get install ssh
sudo shutdown -P now
```
10. Finished

## 4. Setting up the host computer ##

### Linux ###
```
nohup VBoxHeadless -s host-vm-name > /dev/null &
```
If you use <code>dnsmasq</code>, it might need to be restarted.
```
service dnsmasq restart
```

### Windows 10 Anniversary  ###
1. Open Settings -> Update & Security -> For developers -> Select Developer mode radio option.
2. Control panel -> Programs -> Turn Windows features on or off -> enable: Windows Subsytem for Linux (Beta)
3. Reboot
4. Start bash and install linux.
5. Start the vm.
6. Start <code>Bash on Ubuntu on Windows</code> (Later on refered to as "terminal").
	1. To enable quick edit mode, right click window title, select properties, and check: Quick edit mode. To copy, make selection and (press enter or right click) to copy. Right click without a selection to paste.
7. Enter: ```ssh host-vm-name```.
8. Install samba.
	1. ```sudo apt-get install samba```
	2. ```sudo smbpasswd -a username```
	3. Enter your samba password.
	4. ```sudo nano /etc/samba/smb.conf``` Add to the end:
```
[username]
path = /home/username
valid users = username
read only = no
create mask = 664
force create mode = 664
security mask = 664
force security mode = 664
directory mask = 0775
force directory mode = 0775
directory security mask = 0775
force directory security mode = 0775
```
	5. ```sudo shutdown -P now```
9. Create a new file <code>Start vm name.bat</code>
```
@echo off
"C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" startvm "host-vm-name" --type headless
timeout 20 > NUL
net use Z: \\host-vm-name\username
```

## 5. Setting up the vm ##
1. Start a terminal
2. Setting up autologin:
	1. If you do not already have a id_rsa.pub, generate one: ```ssh-keygen```
	2. ```scp .ssh/id_rsa.pub host-vm-name:/home/username/host-vm-name.key```.
	3. ```ssh host-vm-name```.
	4. ```cat host-vm-name.key > .ssh/authorized_keys``` (if the folder does not exist, do 5.4 instead of later).
	5. ```rm host-vm-name.key```
	6. <kbd>^D</kbd>
3. Log into your vm: ```ssh host-vm-name```.
4. Generate a ssh key: ```ssh-keygen```.
5. Setting your preferred editor: ```sudo update-alternatives --config editor```.
6. Setup visudo.
	1. ```sudo visudo```
	2. Add: ```username ALL=(ALL) NOPASSWD:ALL```
7. Updating the system.
```
sudo su -
apt-get update && apt-get dist-upgrade
```
<kbd>^D</kbd>
8. Setting up a git friendly prompt.
	1. ```editor .bashrc```
	2. Locate:
```
if [ "$color_prompt" = yes ]; then
	PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
	PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt
```
	3. Replace with:
```
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;36m\]\w\[\033[00m\]$(__git_ps1 " [\[\033[00;33m\]%s\[\033[00m\]] ")\$ '
```
	4. <kbd>^D</kbd>
	5. ```ssh host-vm-name```.
9. Adding yourself to the <code>users</code> group.
	1. ```sudo usermod -a -G users username```
	2. <kbd>^D</kbd>
	3. ```ssh host-vm-name```.
10. Turn off the vm: ```shutdown -P now```.

## 6. Backing up the vm ##
1. Locate the <code>.vdi</code> file.
	1. Linux: <code>/home/username/VirtualBox VMs/host-vm-name/host-vm-name.vdi</code>.
	2. Windows: User > VirtualBox VMs > <code>host-vm-name.vdi</code>
2. Take a copy of the <code>.vdi</code> file to a safe location.
