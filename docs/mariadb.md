# Secure mariadb and Configure (optional)

## Harden mariadb

Harden the mariadb instance by running 
```bash
sudo mysql_secure_installation
```

The `root` account's default password is not set so hit enter when prompted for the current password.

- Change the `root` user's password.
- Do not switch to unix socket based authentication.
- Remove test database.
- Disable anonymous access.

Configure the mariadb listening IP address from localhost.

```bash
sudo vi /etc/mysql/mariadb.conf.d/50-server.cnf
```

Change the bind-address to 0.0.0.0

```ini
bind-address = 0.0.0.0
```

Restart mariadb

```bash
sudo service mariadb stop && sudo service mariadb start
```

## Create motionplus database

Create a new database for motionplus

```bash
sudo mariadb
```

```sql
CREATE DATABASE motionplus;

SHOW DATABASES;
```

Create a new `motionplus` user, set its password, and grant access to the `motionplus` database. Note in the SQL `CREATE USER` command, replace your network subnet for the `192.168.xxx.0` and `<password>` with your password.

```bash
sudo mariadb
```

```sql

CREATE USER 'motionplus'@'192.168.xxx.0/255.255.255.0' IDENTIFIED BY '<password>';
CREATE USER 'motionplus'@localhost IDENTIFIED BY '<password>';

FLUSH PRIVILEGES;

SELECT host, user FROM mysql.user;

CREATE DATABASE motionplus;

GRANT ALL PRIVILEGES ON motionplus.* to 'motionplus'@'192.168.xxx.0/255.255.255.0';
GRANT ALL PRIVILEGES ON motionplus.* to 'motionplus'@localhost;

FLUSH PRIVILEGES;

SHOW GRANTS FOR 'motionplus'@'192.168.xxx.0/255.255.255.0';
SHOW GRANTS FOR 'motionplus'@localhost;
```

When motionplus starts and connects to the database, it will create the `motionplus` table in the `motionplus` database.

## Test the configuration

Run `motionplus` from the command line and check the logs.

```bash
sudo /usr/local/bin/motionplus -c /etc/motionplus/motionplus.conf
```

Review the runtime log.

```bash
sudo tail -f /var/log/motionplus/motionplus.log
```

Next Step: [Install MotionPlus](./install-motionplus.md)
