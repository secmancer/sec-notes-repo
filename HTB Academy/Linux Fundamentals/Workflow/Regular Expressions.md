Regular expressions (RegEx) are a powerful tool for searching and manipulating text based on specific patterns. Here's a breakdown of the key concepts and examples discussed:
Grouping with Regular Expressions

1. Round Brackets ():

    Used to group parts of a regex.
    Example: (my|false) searches for lines containing either "my" or "false."

2. Square Brackets []:

    Define character classes, specifying a list of characters to search for.
    Example: [a-z] matches any lowercase letter from a to z.

3. Curly Brackets {}:

    Define quantifiers, indicating how often a previous pattern should be repeated.
    Example: {1,10} means the pattern should repeat between 1 to 10 times.

4. OR Operator |:

    Matches results when one of the given expressions is found.
    Example: grep -E "(my|false)" /etc/passwd searches for lines containing either "my" or "false."

5. AND Operator .*:

    Matches results only if both expressions are found.
    Example: grep -E "(my.*false)" /etc/passwd searches for lines containing both "my" and "false" in that order.

![[Screenshot_20240812_140725 1.png]]
### **Usage in Tools**

- **Grep** and **Sed** are common tools that use regular expressions for searching and replacing text.
- Regular expressions are also widely used in web applications for validating user input, making them a critical skill in many areas of programming and cybersecurity.

By mastering regular expressions, you'll be able to efficiently search, filter, and manipulate text data in a variety of contexts, making it a valuable tool in your toolkit.