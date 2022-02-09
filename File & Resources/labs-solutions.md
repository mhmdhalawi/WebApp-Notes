# Reverse shell

Check if you can upload a **.php** file to the server, if not you can change the extension to **.jpg** and intercept it with burp suite to change it back to **.php**

Find a script for reverse shell based on languange (php, python, ruby, perl, bash, etc) for this example we will use **PHP**.

Copy the script to a file and upload it to the server.(name it shell.php)

https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php


Change the ip and port to your own 

Type in the cmd **ifconfig** to find the ip address connected to the server/network. If the ip is 10.100.13.200 then change the **IP** in the script file to it.

    IP  : 10.100.13.200

    Port : 1234

Go to this link for the tutorial

https://pentestmonkey.net/tools/web-shells/php-reverse-shell

After uploading the script click on it in the browser and then type in the cmd **nc -nvlp 1234** to listen for the reverse shell. 

    nc -nvlp 1234

In the command line from the shell type this command to find the session_save_path:

    php -r 'echo session_save_path(), "\n";' 

Finally you can check the directory with **ls** and print the content with **cat**.

    ls 
    cat [file name]

<br/>

# One Liner Php shell

Search for **One Liner Php Shell** on google and download it.

    https://gist.github.com/sente/4dbb2b7bdda2647ba80b

Usage:

    <!-- http://target.com/simple-backdoor.php?cmd=cat+/etc/passwd -->