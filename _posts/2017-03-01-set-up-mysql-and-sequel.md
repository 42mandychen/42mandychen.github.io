---
layout: post
title: Set up MySQL and Sequel Pro on macOS
date:   2017-03-01 20:00:01 -0600
excerpt: Steps I took to set up MySQL and Sequel Pro on my laptop.
---

# Set up MySQL and Sequel Pro on macOS

1. Download and install [MYSQL Community Server](https://dev.mysql.com/downloads/mysql/)

   - Remember the password you get after successfully installing MySQL.

2. Start the server: System Preferences —> MySQL —> Start MySQL Server

3. Open Terminal and type

   ```
   $ cd /usr/local/mysql/bin
   $ ./mysql -u root -p
   ```

   //at this point, type the password you got

   ```
   $ SET PASSWORD FOR 'root'@'localhost' = PASSWORD('your own password');
   ```

   //replace 'your won password' with your new password

   ```
   $ ALTER USER 'root'@'localhost' PASSWORD EXPIRE NEVER;
   ```

4. Download and install [Sequel Pro](https://sequelpro.com/download)

5. Open Sequel Pro and ollow the [instructions](https://sequelpro.com/docs/get-started/get-connected/local-mysql) to connect with MySQL server on



### Reference

[Set up MySQL on Mac OS X 10.11 - Tutorial](https://www.youtube.com/watch?v=q9S51sykd1A)
