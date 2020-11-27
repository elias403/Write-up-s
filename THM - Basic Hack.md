<h1>We start with a scan: **nmap -A -sC ip**
We see an Apache server and an FTP server. It is possible to enter ftp with **user anonymous**, without a password.</h1>

![nmap](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/1.PNG)</h1>

<h1>Going to the Browser *http://ip_target* we see a default Apache page, there is a comment in the source code.</h1>

![browser](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/2.png)

<h1>Using **gobuster**, we discovered a hidden directory, with a file called CALL.txt

![gobuster](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/3.png)

<h1>Now we will go to *FTP*

![ftp, anonymous](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/4.PNG)

With **ls -la** we see that we can * write to the FTP directory * and that it is the same folder where the CALL.txt file is located.
We can use /usr/share/webshells/php/php-reverse-shell.php
We just need to change the ip and port before uploading to FTP

![php-reverse-shell](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/5.PNG)

We will send php-reverse-shell.php to the victim via ftp -> ** put xx/php-reverse-shell.php **

![put_php-reverse-shell](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/6.PNG)

Let's open ¹**nc -lnvp 1234** by listening and go to the ?browser to open ³php-reverse-shell.php

![nc](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/7.PNG)
![browser](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/8.PNG)
![conexão](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/9.PNG)

We found the 1st flag in /home/shrek/user.txt

![flag1](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/10.PNG)

<h2>In / home, we see an important.txt file, pointing to "/.runme.sh"</h2>

![runme.sh](https://github.com/elias403/Write-up-s/blob/main/images/THM%20-%20Basic%20Hack/11.png)

Analyzing ¹hash, it is an MD5, we see that it is possibly the credential for ²SSH and also the secret key
https://www.tunnelsup.com/hash-analyzer/
https://crackstation.net/

![shrek:hash](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/12.PNG)
![ssh](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/13.PNG)

By providing sudo -l, we can run python with sudo without a password. Going to https://gtfobins.github.io/gtfobins/python/#sudo, we see a way to get a privileged shell.

![sudo-l](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/14.PNG)

'''
sudo python -c 'import os; os.system("/bin/sh")'
'''

![root](https://raw.githubusercontent.com/elias403/Write-up-s/main/images/THM%20-%20Basic%20Hack/15.PNG)


