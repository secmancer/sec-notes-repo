### Introduction
- **Regular Expressions (RegEx)** are a powerful tool for searching, analyzing, and manipulating text by defining search patterns.
- They are commonly used for tasks like finding and replacing text, validating input, and analyzing data.
- RegEx consists of a sequence of **letters and symbols** forming a search pattern, often including **metacharacters** that define patterns without literal meaning.
- RegEx is widely supported across programming languages and tools like `grep` and `sed`.
- Web applications frequently implement RegEx for **user input validation**.



### Grouping
- Among other things, regex offers us the possibility to group the desired search patterns. 
- Basically, regex follows three different concepts, which are distinguished by the three different brackets:
- #### Grouping Operators
![[Screenshot_20241108_200830.png]]
- Suppose we use the `OR` operator. 
- The regex searches for one of the given search parameters.
- In the next example, we search for lines containing the word `my` or `false`. 
- To use these operators, you need to apply the extended regex using the `-E` option in grep
- #### OR operator
```shell-session
cry0l1t3@htb:~$ grep -E "(my|false)" /etc/passwd

lxd:x:105:65534::/var/lib/lxd/:/bin/false
pollinate:x:109:1::/var/cache/pollinate:/bin/false
mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```
- Since one of the two search parameters always occurs in the three lines, all three lines are displayed accordingly. 
- However, if we use the `AND` operator, we will get a different result for the same search parameters.
- #### AND operator
```shell-session
cry0l1t3@htb:~$ grep -E "(my.*false)" /etc/passwd

mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```
- Basically, what we are saying with this command is that we are looking for a line where we want to see both `my` and `false`. 
- A simplified example would also be to use `grep` twice and look like this:
```shell-session
cry0l1t3@htb:~$ grep -E "my" /etc/passwd | grep -E "false"

mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```
- Here are some optional tasks to practice regex that can help us to handle it better and more efficiently. 
- For all exercises, we will use the `/etc/ssh/sshd_config` file on our `Pwnbox` instance.
![[Screenshot_20241108_200948.png]]
