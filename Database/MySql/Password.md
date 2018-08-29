# MySQL command

## Stop MySQL
The first thing to do is stop MySQL. If you are using Ubuntu or Debian the command is as follows:

```sudo /etc/init.d/mysql stop```

For CentOS, Fedora, and RHEL the command is:

```sudo /etc/init.d/mysqld stop```

Safe mode
Next we need to start MySQL in safe mode - that is to say, we will start MySQL but skip the user privileges table. Again, note that you will need to have sudo access for these commands so you don't need to worry about any user being able to reset the MySQL root password:

```sudo mysqld_safe --skip-grant-tables &```

Note: The ampersand (&) at the end of the command is required.

Login
All we need to do now is to log into MySQL and set the password.

```mysql -uroot```

Note: No password is required at this stage as when we started MySQL we skipped the user privileges table.

Next, instruct MySQL which database to use:

```use mysql;```

Reset Password
Enter the new password for the root user as follows:

```update user set password=PASSWORD("mynewpassword") where User='root';```

and finally, flush the privileges:

```flush privileges;```

Restart
Now the password has been reset, we need to restart MySQL by logging out:

quit
and simply stopping and starting MySQL.

On Ubuntu and Debian:

```sudo /etc/init.d/mysql stop```

```sudo /etc/init.d/mysql start```

On CentOS and Fedora and RHEL:

```sudo /etc/init.d/mysqld stop```

```sudo /etc/init.d/mysqld start```

Login
Test the new password by logging in:

```mysql -u root -p```


> ```mysql> SELECT 1;```
ERROR 1820 (HY000): You must SET PASSWORD before executing this statement

> mysql> SET PASSWORD = PASSWORD('new_password');
> Query OK, 0 rows affected (0.01 sec)