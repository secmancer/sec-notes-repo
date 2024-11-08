- In the last section, we learned about the redirections we can use to redirect results from one program to another for processing. 
- To read files, we do not necessarily have to use an editor for that. 
- There are two tools called `more` and `less`, which are very identical. These are fundamental `pagers` that allow us to scroll through the file in an interactive view. Let us have a look at some examples.


### More
```shell-session
secmancer@htb[/htb]$ more /etc/passwd
```
- After we read the content using `cat` and redirected it to `more`, the already mentioned `pager` opens, and we will automatically start at the beginning of the file.
```shell-session
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
<SNIP>
--More--
```
- With the `[Q]` key, we can leave this `pager`. We will notice that the output remains in the terminal.


