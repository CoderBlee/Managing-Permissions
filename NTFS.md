# NTFS Permissions using PowerShell

This lab teaches you how to manage NTFS permissions using **PowerShell** and the **icacls** command, which is very powerful for controlling file access in Windows

---

1. **Open PowerShell as Administrator**  
   - Click on **Start**, type `PowerShell`, right-click **Windows PowerShell**, and select **Run as Administrator**.  
   - Confirm by clicking **Yes** on the User Account Control (UAC) prompt.

2. **Navigate to the File Directory**  
   - Use the `cd` (Change Directory) command to move to the folder containing the file:  
     ```powershell
     cd c:\LABFILES
     ```

3. **View Current NTFS Permissions**  
   - Use `icacls` to list the current permissions on `comptia-logo.jpg`:  
     ```powershell
     icacls .\comptia-logo.jpg
     ```
   Example output:  
   ```
   comptia-logo.jpg NT AUTHORITY\SYSTEM:(I)(F)
                   BUILTIN\Administrators:(I)(F)
                   LABDOMAIN\dylan:(R)
   ```

   Explanation:  
   - `(F)` = Full Control  
   - `(R)` = Read  
   - `(I)` = Inherited permission  

---

### **Deny Read Permission to a User**  
The `/deny` option explicitly denies permissions. This overrides any inherited permissions.  
- Command:  
  ```powershell
  icacls .\comptia-logo.jpg /deny dylan:R
  ```
- Check the results:  
  ```powershell
  icacls .\comptia-logo.jpg
  ```
  The output will now show `LABDOMAIN\dylan` with a `(DENY)` flag for read access:  
  ```
  comptia-logo.jpg LABDOMAIN\dylan:(DENY)(R)
  ```

---

### **Grant Full Control to a User**  
To give `dylan` full control over the file:  
- Command:  
  ```powershell
  icacls .\comptia-logo.jpg /grant dylan:F
  ```
- Verify the change:  
  ```powershell
  icacls .\comptia-logo.jpg
  ```
  The output will now show `LABDOMAIN\dylan` with `(F)` for full control.

---

### **Remove Specific Permissions**  
If you want to remove permissions granted to `dylan`, use `/remove` with the `:g` flag:  
- Command:  
  ```powershell
  icacls .\comptia-logo.jpg /remove:g dylan
  ```
- Check the result:  
  ```powershell
  icacls .\comptia-logo.jpg
  ```

---

### **Inheritance Reminder**
Removing specific permissions does **not** mean the user will have no permissions at all. **Inherited permissions** from groups (e.g., Administrators) or parent folders will still apply unless explicitly overridden. This is an important concept for managing NTFS permissions.

---

### **Summary of Common icacls Commands:**

| Command                              | Explanation                          |
|--------------------------------------|--------------------------------------|
| `icacls file`                        | View current permissions             |
| `icacls file /grant user:F`          | Grant full control                   |
| `icacls file /deny user:R`           | Deny read access                     |
| `icacls file /remove:g user`         | Remove specific granted permissions  |
| `icacls file /reset`                 | Reset permissions to default         |

