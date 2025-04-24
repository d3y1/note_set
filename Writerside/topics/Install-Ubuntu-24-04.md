# Install Ubuntu-24.04

```powershell
PS C:\Users\admin> wsl -l -o
以下是可安装的有效分发的列表。
使用 'wsl.exe --install <Distro>' 安装。

NAME                            FRIENDLY NAME
AlmaLinux-8                     AlmaLinux OS 8
AlmaLinux-9                     AlmaLinux OS 9
AlmaLinux-Kitten-10             AlmaLinux OS Kitten 10
Debian                          Debian GNU/Linux
SUSE-Linux-Enterprise-15-SP5    SUSE Linux Enterprise 15 SP5
SUSE-Linux-Enterprise-15-SP6    SUSE Linux Enterprise 15 SP6
Ubuntu                          Ubuntu
Ubuntu-24.04                    Ubuntu 24.04 LTS
kali-linux                      Kali Linux Rolling
openSUSE-Tumbleweed             openSUSE Tumbleweed
openSUSE-Leap-15.6              openSUSE Leap 15.6
Ubuntu-18.04                    Ubuntu 18.04 LTS
Ubuntu-20.04                    Ubuntu 20.04 LTS
Ubuntu-22.04                    Ubuntu 22.04 LTS
OracleLinux_7_9                 Oracle Linux 7.9
OracleLinux_8_7                 Oracle Linux 8.7
OracleLinux_9_1                 Oracle Linux 9.1

PS C:\Users\admin> wsl --install -d Ubuntu-24.04
正在下载: Ubuntu 24.04 LTS
正在安装: Ubuntu 24.04 LTS
已成功安装分发。它可通过 “wsl.exe -d Ubuntu-24.04” 启动

PS C:\Users\admin> wsl.exe -d Ubuntu-24.04
Provisioning the new WSL instance Ubuntu-24.04
This might take a while...
Create a default Unix user account: admin
fatal: The group `admin' already exists.
Failed to create user 'admin'. Please choose a different name.
Create a default Unix user account: ubt
New password:
Retype new password:
passwd: password updated successfully
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

Welcome to Ubuntu 24.04.2 LTS (GNU/Linux 5.15.167.4-microsoft-standard-WSL2 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Tue Mar 18 16:33:01 CST 2025

  System load:  0.02                Processes:             31
  Usage of /:   0.1% of 1006.85GB   Users logged in:       0
  Memory usage: 2%                  IPv4 address for eth0: 172.29.194.128
  Swap usage:   0%


This message is shown once a day. To disable it please create the
/home/ubt/.hushlogin file.

ubt@DESKTOP-NE448JV:/mnt/c/Users/admin$
ubt@DESKTOP-NE448JV:/mnt/c/Users/admin$ pwd
/mnt/c/Users/admin
ubt@DESKTOP-NE448JV:/mnt/c/Users/admin$

// 列出list
PS C:\Users\admin> wsl.exe -l -v
  NAME              STATE           VERSION
* docker-desktop    Running         2
  Ubuntu-24.04      Running         2

// 卸载wsl Ubuntu-24.04
PS C:\Users\admin> wsl --list -verbose
PS C:\Users\admin> wsl --unregister Ubuntu-24.04
PS C:\Users\admin> wsl --list -verbose

```
{collapsible="true" collapsed-title="Install Ubuntu-24.04 commands on powershell with wsl2" default-state="expanded"}