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

not sure why mysql-client mysql-server won't do `sudo apt-get install mysql-client mysql-server` you could add ` -y` I guess to skip questions.

```bash
pi@raspberry:~ $ sudo mysql -p
Enter password: <empty password by default>
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 3
Server version: 10.1.26-MariaDB-0+deb9u1 Debian 9.1

Copyright (c) 2000, 2017, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> SELECT DATABASE();
+------------+
| DATABASE() |
+------------+
| NULL       |
+------------+
1 row in set (0.00 sec)

MariaDB [(none)]> exit
Bye
```

# Apache

[reference](https://www.cyberciti.biz/faq/how-to-install-linux-apache-mysql-php-lamp-stack-on-debian-9-stretch/)

Install apache by:
`sudo apt-get install apache2 -y`

Now you can open up a browser window from shell:

`chromium localhost`

And press ALT+F4 to close the window again

# PHP
