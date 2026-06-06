# Safe Commands Reference

This file documents the main Linux and database commands used in the project. Passwords and sensitive values are replaced with placeholders.

## Install LAMP Stack Packages
```bash
sudo dnf install -y httpd mariadb105-server wget php-fpm php-mysqli php-json php php-devel
```

## Start and Enable Services
```bash
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd

sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo systemctl status mariadb
```

## Secure MariaDB
```bash
sudo mysql_secure_installation
```

Use a strong password and avoid committing any passwords to GitHub.

## Create WordPress Database and User
```sql
CREATE DATABASE wordpress_db;
CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY '<strong-password>';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## Test PHP
```bash
sudo nano /var/www/html/phpinfo.php
```

```php
<?php phpinfo(); ?>
```

Access the test page using:

```text
http://<public-ip>/phpinfo.php
```

Remove this file after testing in a real deployment:

```bash
sudo rm /var/www/html/phpinfo.php
```

## Install WordPress
```bash
cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xzf latest.tar.gz
sudo cp wordpress/wp-config-sample.php wordpress/wp-config.php
sudo nano wordpress/wp-config.php
```

Update `wp-config.php` with the database name, user, and password using safe placeholder values.
