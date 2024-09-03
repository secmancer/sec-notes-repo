**PowerShell Output (Objects Explained)**

With PowerShell, everything is treated as an object, unlike traditional command-line interfaces that handle output as plain text. Here’s an overview of what objects mean in PowerShell:

- **What is an Object?**  
    An object is an individual instance of a class in PowerShell. For example, think of a computer as an object—its components and functions combined define it.
    
- **What is a Class?**  
    A class is like a blueprint that defines the structure and behavior of objects. It outlines what properties and methods the objects will have.
    
- **What are Properties?**  
    Properties are the attributes or data associated with an object. For a computer object, properties could include things like CPU, RAM, or storage.
    
- **What are Methods?**  
    Methods are the actions or functions that an object can perform. For example, a computer can perform tasks like processing data or running applications, which would be considered methods.
    

By understanding these concepts, you can better work with and manipulate objects in PowerShell.

---

**Finding and Filtering Objects**

Let’s look at how to work with user objects in PowerShell.

- **Get an Object (User) and its Properties/Methods**  
    You can retrieve a user object and examine its properties and methods by using the `Get-LocalUser` cmdlet followed by `Get-Member`. This will list all the properties and methods associated with the user object.
    
- **Property Output (All)**  
    To see all properties of a user object, you can use the `Select-Object` cmdlet with the `-Property *` option. This will display all the properties of the user, such as `Name`, `Enabled`, `LastLogon`, etc.
    
- **Filtering on Properties**  
    If you only want to see specific properties, you can filter the output by selecting just those properties. For example, to see only the `Name` and `PasswordLastSet` properties, use `Select-Object` with those specific properties.
    
- **Sorting and Grouping**  
    You can sort and group objects based on their properties using `Sort-Object` and `Group-Object`. For instance, you can sort users by their `Name` and group them by whether they are `Enabled` or not.
    

This way, you can easily manage and manipulate the data associated with objects in PowerShell.

---

**Why Do We Need to Filter our Results?**

Sometimes, the output from PowerShell commands can be overwhelming. For example, when working with services, you might get a large amount of data that’s difficult to sift through.

- **Too Much Output**  
    If you run `Get-Service` and try to display all properties, you’ll get a lot of information, such as `DisplayName`, `ServiceName`, `Status`, and more.
    
- **Finding & Filtering Content**  
    To make the output more readable, you can filter it by selecting only the properties you’re interested in, like `DisplayName`, `Name`, and `Status`. You can also sort the results by `DisplayName` and format the output as a list for easier reading.
    

If you’re looking for something specific, such as whether a service related to `Windows Defender` is running, you can use `Where-Object` to filter the results based on the `DisplayName` property.


### Questions
- What defines the functions our objects have?
	- Methods
- What Cmdlet can show us the properties and methods of an object?\
	- Get-Member
- If we wanted to look through a directory and all sub-directories for something, what modifier would we use with the Get-ChildItem Cmdlet?
	-  -Recurse