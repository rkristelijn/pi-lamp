# Install LAMP on raspbian x86

1. Download / install VirtualBox
2. download x86 version of [raspbian](https://www.raspberrypi.org/downloads/raspberry-pi-desktop/) - current build, as per date of writing: Stretch 2018-06-27 Kernel 4$
3. Type: Linux, Version: Debian (64-bit), 4096MB Mem, new harddisk, 32 GB, VDI, dynamically
4. Settings: no floppy, mount optical to iso, upgrade CPU to 2
5. Follow install instructions of Debian 9
6. Install Guest addition: mount the guest edition iso file from the menu or manually (c:\program files\oracle\virtualbox\*.iso) go to console `sudo /media/cdrom/VBoxL$
7. good point to make a backup, exporting the appliance

Note: somehow on my system Virtual

# Tools
What good is a machine to a developer without a proper editor? [Visual Studio Code](https://code.visualstudio.com/docs/?dv=linux32_deb)

```bash
pi@raspberry:~/Downloads $ sudo dpkg -i code_1.26.1-1534444677_i386.deb
```

# MySQL

[reference](https://linuxconfig.org/how-to-install-mysql-community-server-on-debian-9-stretch-linux)

not sure why mysql-client mysql-server won't do `sudo apt-get install mysql-client mysql-server`

```bash
raspbian-stretch-clean-install
```
