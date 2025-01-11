### Notes on Decoding Encoded Strings

#### **Overview**
- Encoded text is often used in obfuscated scripts to make it less human-readable and harder to analyze. 
- Decoding such strings is an essential skill for reverse engineering obfuscated code. 
- Below are some common encoding techniques and how to handle them.



### **1. Base64 Encoding**
- #### **Characteristics**:
- Uses only alphanumeric characters, plus `+` and `/`.
- Padded with = to ensure the string length is a multiple of 4.
- #### **Commands**:
- **Encoding**:
    ```bash
    echo "text" | base64
    ```
- Example:
    ```bash
    echo "https://www.hackthebox.eu/" | base64
    ```
- Output:
    ```
    aHR0cHM6Ly93d3cuaGFja3RoZWJveC5ldS8K
    ```
- **Decoding**:
    ```bash
    echo "encoded_text" | base64 -d
    ```
- Example:
    ```bash
    echo "aHR0cHM6Ly93d3cuaGFja3RoZWJveC5ldS8K" | base64 -d
    ```
- Output:
    ```
    https://www.hackthebox.eu/
    ```



#### **Use Case**:
- The string `ZG8gdGhlIGV4ZXJjaXNlLCBkb24ndCBjb3B5IGFuZCBwYXN0ZSA7KQo=` from the previous section is base64-encoded.
- **Decoding Command**:
```bash
echo "ZG8gdGhlIGV4ZXJjaXNlLCBkb24ndCBjb3B5IGFuZCBwYXN0ZSA7KQo=" | base64 -d
```



### **2. Hex Encoding**
- #### **Characteristics**:
	- Encodes characters into their hexadecimal ASCII values.
	- Uses only characters `0-9` and `a-f`.
- #### **Commands**:
	- **Encoding**:
    ```bash
    echo "text" | xxd -p
    ```
	- Example:
    ```bash
    echo "https://www.hackthebox.eu/" | xxd -p
    ```
	- Output: 
    ```
    68747470733a2f2f7777772e6861636b746865626f782e65752f0a
    ```
	- **Decoding**:
    ```bash
    echo "hex_string" | xxd -p -r
    ```
    - Example:
    ```bash
    echo "68747470733a2f2f7777772e6861636b746865626f782e65752f0a" | xxd -p -r
    ```
    - Output:
    ```
    https://www.hackthebox.eu/
    ```
    


### **3. Rot13 (Caesar Cipher)**
- #### **Characteristics**:
	- Shifts each letter by a fixed number (rot13 shifts by 13).
	- A simple substitution cipher, easily reversible.
- #### **Commands**:
	- **Encoding/Decoding**:
    ```bash
    echo "text" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
    ```
    - Example:
    ```bash
    echo "https://www.hackthebox.eu/" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
    ```
    - Output:
    ```
    uggcf://jjj.unpxgurobk.rh/
    ```
	- To decode, run the same command:
    ```bash
    echo "uggcf://jjj.unpxgurobk.rh/" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
    ```
    - Output:
    ```
    https://www.hackthebox.eu/
    ```



### **4. Identifying Encoding Types**
- **Spotting Base64**:
    - Contains alphanumeric characters, `/`, `+`, and `=`.
    - String length is a multiple of 4.
- **Spotting Hex**:
    - Contains only characters `0-9` and `a-f`.
    - Represents ASCII values.
- **Spotting Rot13**:
    - Looks like random text but retains patterns (e.g., URLs may appear scrambled but recognizable).

#### **Tools**:

- **Cipher Identifier**:
    - A tool to help identify unknown encodings.
    - Use online or standalone versions.

---

### **5. Advanced Cases: Encryption**

- Some obfuscated scripts use encryption (e.g., AES, RSA).
- Decoding requires the encryption key.
- If the key is not stored in the script, decryption becomes significantly harder.

---

### **Key Takeaways**

1. Familiarize yourself with common encoding methods: Base64, Hex, and Rot13.
2. Use Linux commands to quickly encode or decode text.
3. For unknown encodings, start by identifying patterns or use tools like Cipher Identifier.
4. Encryption adds complexity and often requires access to keys for successful decryption.



### Questions
- Using what you learned in this section, determine the type of encoding used in the string you got at previous exercise, and decode it. To get the flag, you can send a 'POST' request to 'serial.php', and set the data as "serial=YOUR_DECODED_OUTPUT".
	- HTB{ju57_4n07h3r_r4nd0m_53r14l}