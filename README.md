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

The system configures Apache to start automatically after boot.

Take note of `sudo mysql_secure_installation`

If we skip this, we can't create databases in phpmyadmin

# PHP

`sudo apt install php7.0 libapache2-mod-php7.0 php7.0-mysql php7.0-gd php7.0-opcache -y`

`sudo systemctl restart apache2` needed? -> Nope
`sudo vi /var/www/html/phpinfo.php`

```php
<?php phpinfo(); ?>
```

`chromium localhost/phpinfo.php`

# PHPMyAdmin

[reference](https://pimylifeup.com/raspberry-pi-mysql-phpmyadmin/)

`sudo apt-get install phpmyadmin -y`

complete wizard
e.g. I used 'admin' as password for user phpmyadmin

`sudo nano /etc/apache2/apache2.conf`
7b. Now at the bottom of this file enter the following line:

`Include /etc/phpmyadmin/apache.conf`
Once done save & exit by pressing CTRL +X and then y.

Now restart the Apache service by entering the following command:

`sudo /etc/init.d/apache2 restart`

`chromium localhost/phpmyadmin` phpmyadmin:admin

phpmyadmin can't create databases, and won't allow root to login to phpmyadmin. 

Solutions:
1. allow database creation by phpmyadmin user...
2. Update AllowNoPassword
3. Set pw for root

I choose 1

```bash
pi@raspberry:/etc/phpmyadmin $ sudo mysql -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 10
Server version: 10.1.26-MariaDB-0+deb9u1 Debian 9.1

Copyright (c) 2000, 2017, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> GRANT ALL PRIVILEGES ON * . * TO 'phpmyadmin'@'localhost';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> 

```

# Configuring MySQL

[references](https://www.digitalocean.com/community/tutorials/how-to-create-a-new-user-and-grant-permissions-in-mysql)

```bash

```

```SQL
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
FLUSH PRIVILEGES;
```

`/var/www/html/mysqltest.php`
```php
/*
** Connect to database:
*/
 
// connect to the database
$con = mysql_connect('localhost','newuser','password') 
    or die('Could not connect to the server!');
 
// select a database:
mysql_select_db('testdb') 
    or die('Could not select a database.');
 
 
/*
** Fetch some rows from database:
*/
 
// read username from URL
$username = $_GET['username'];
 
// escape bad chars:
$username = mysql_real_escape_string($username);
 
// build query:
$sql = "SELECT id, timestamp, text FROM logs WHERE username = '$username'";
 
// execute query:
$result = mysql_query($sql) 
    or die('A error occured: ' . mysql_error());
 
// get result count:
$count = mysql_num_rows($result);
print "Showing $count rows:<hr/>";
 
// fetch results:
while ($row = mysql_fetch_assoc($result)) {
    $row_id = $row['id'];
    $row_text = $row['text'];
 
    print "#$row_id: $row_text<br/>\n";
}
 
 
/*
** Do a insert query:
*/
 
// create SQL query:
$sql = "INSERT INTO logs (timestamp, text) VALUES (NOW(), 'some text here!')";
 
// execute query:
$result = mysql_query($sql) or die('A error occured: ' . mysql_error());
 
// get the new ID of the last insert command
$new_id = mysql_insert_id();
 
 
 
/*
** Do a update query:
*/
 
// create SQL query:
$sql = "UPDATE logs SET text='New text!' WHERE id='1'";
 
// execute query:
$result = mysql_query($sql) or die('A error occured: ' . mysql_error());
 
 
 
/*
** Do a delete query:
*/
 
// create SQL query:
$sql = "DELETE FROM logs WHERE id='1'";
 
// execute query:
$result = mysql_query($sql) or die('A error occured: ' . mysql_error());
 
 
 
// Have fun!
```

# Import DB

# SSL / HTTPS
[reference](https://hallard.me/enable-ssl-for-apache-server-in-5-minutes/)