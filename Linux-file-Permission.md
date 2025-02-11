# Linux file permissions

### **Step-by-Step Guide:**
1. **Check Current Directory**  
   - Command: `pwd`  
   This will confirm that you're in the `/root` directory. If not, use `cd ~` to move to the root’s home directory.

2. **View File Permissions**  
   - Command: `ls -l`  
   This displays a detailed list of files with permissions, owners, and other information. Focus on the **first 10 characters** of each line, which represent the file type and permissions.

   Example output:  
   ```
   -rw-r--r--  1 root root  1024 Feb 10 12:00 demofile.sh
   ```

   Explanation:  
   - `-rw-r--r--`: File permissions.  
   - First `-`: Indicates it's a file (`d` if it’s a directory).  
   - Next three `rw-`: Owner has read and write access.  
   - Next three `r--`: Group has read-only access.  
   - Last three `r--`: Others have read-only access.  

3. **Apply Permissions Changes**  

   **Use chmod commands to set proper permissions for `demofile.sh`:**
   
   - **Grant full access to the owner, execute access to the group, and no access to others:**  
     ```bash
     chmod 710 demofile.sh
     ```

     This sets permissions to:  
     - Owner (`rwx`) – full access (read, write, execute).  
     - Group (`--x`) – only execute permission.  
     - Others (`---`) – no access.  

   - **Verify the changes:**  
     ```bash
     ls -l demofile.sh
     ```
     You should see:  
     ```
     -rwx--x---  1 root root  1024 Feb 10 12:00 demofile.sh
     ```

4. **Test the Script**  
   Run the script to see what it does:  
   ```bash
   ./demofile.sh
   ```
   If it’s a shell script with an important function, it will execute and show the output.

5. **View the Script’s Code**  
   To inspect the contents of `demofile.sh`, use:  
   ```bash
   cat demofile.sh
   ```

---

### **Octal Permissions Summary**
When using `chmod` with a numeric (octal) representation:  

| Permission | Octal Value | Meaning         |
|------------|-------------|----------------|
| ---        | 0           | No access      |
| --x        | 1           | Execute only   |
| -w-        | 2           | Write only     |
| -wx        | 3           | Write + Execute |
| r--        | 4           | Read only      |
| r-x        | 5           | Read + Execute |
| rw-        | 6           | Read + Write   |
| rwx        | 7           | Full access    |

**Example:** `chmod 740 file.sh`  
- Owner (`7`) = `rwx`  
- Group (`4`) = `r--`  
- Others (`0`) = `---`  

---

### **In Your Case:**

1. **Initial permission check** with `ls -l demofile.sh`.  
   If the permissions are `-rwxrwxrwx`, we’ll fix them using `chmod 710`.  

2. **Apply new permissions** to `demofile.sh`:  
   ```bash
   chmod 710 demofile.sh
   ```

3. **Confirm the result** with:  
   ```bash
   ls -l demofile.sh
   ```

---
