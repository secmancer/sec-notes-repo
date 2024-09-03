ChatGPT

This section introduces various Unix/Linux command-line tools that are essential for handling and processing text files efficiently. These tools help you filter, view, and manipulate file contents directly from the terminal without needing an editor. Here's a summary of the tools covered:
1. More

    Usage: more /etc/passwd
    Purpose: Opens a file in a pager that allows you to scroll through the file interactively. Press [Q] to quit. The output remains on the terminal after exiting.

2. Less

    Usage: less /etc/passwd
    Purpose: Similar to more, but with more features. Allows you to scroll and search through a file. Press [Q] to quit, and the output will not remain on the terminal.

3. Head

    Usage: head /etc/passwd
    Purpose: Displays the first ten lines of a file by default. You can change the number of lines with the -n option.

4. Tail

    Usage: tail /etc/passwd
    Purpose: Displays the last ten lines of a file by default. You can also change the number of lines with the -n option.

5. Sort

    Usage: cat /etc/passwd | sort
    Purpose: Sorts the lines in a file alphabetically or numerically.

6. Grep

    Usage:
        cat /etc/passwd | grep "/bin/bash" (Search for specific patterns)
        cat /etc/passwd | grep -v "false\|nologin" (Exclude specific patterns)
    Purpose: Searches for lines containing specific patterns or excludes lines with certain patterns.

7. Cut

    Usage: cat /etc/passwd | grep -v "false\|nologin" | cut -d":" -f1
    Purpose: Cuts out sections from each line of a file based on a delimiter (e.g., :) and a specified field.

8. Tr

    Usage: cat /etc/passwd | grep -v "false\|nologin" | tr ":" " "
    Purpose: Translates or deletes characters from a file, such as replacing all colons with spaces.

9. Column

    Usage: cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | column -t
    Purpose: Formats the output into a table, making it easier to read.

10. Awk

    Usage: cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'
    Purpose: A powerful text processing tool used to manipulate and extract data from files. In this example, it prints the first and last fields of each line.

11. Sed

    Usage: cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | sed 's/bin/HTB/g'
    Purpose: A stream editor for filtering and transforming text. The example replaces all occurrences of "bin" with "HTB".

12. Wc

    Usage: cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | wc -l
    Purpose: Counts the number of lines, words, or characters in a file. The -l option counts the lines.

These tools are foundational for working with text files in a Unix/Linux environment, enabling you to view, filter, modify, and analyze file contents directly from the command line.