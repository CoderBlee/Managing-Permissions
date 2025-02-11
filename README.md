# **Managing Permissions README**

This document outlines the procedures and commands used for managing file permissions on both **Linux** and **Windows** systems. It covers how to view, modify, and understand both **NTFS permissions** and **share permissions** in Windows, and **file permissions** in Linux.

---

## **Linux File Permissions**

### **Viewing File Permissions**
- Use the following command to view the permissions of files in the current directory:
  ```bash
  ls -l
  ```
- This command lists the files and their permissions in the format:
  ```
  -rwxr-xr-x 1 user group size date filename
  ```
  - The first character (`-` or `d`) indicates whether the entry is a file or directory.
  - The next three groups represent permissions for:
    - **User (owner)**
    - **Group**
    - **Others**

### **Modifying File Permissions Using `chmod`**

- **Add execute permission to user:**
  ```bash
  chmod u+x filename
  ```

- **Add write permission to the group:**
  ```bash
  chmod g+w filename
  ```

- **Remove read permission from others and group, remove execute permission from user:**
  ```bash
  chmod go-r,u-x filename
  ```

- **Using octal values to change permissions:**
  - `777`: Full permissions for everyone (rwxrwxrwx)
  - `740`: Full permissions for user, read for group, no permissions for others
  ```bash
  chmod 777 filename
  chmod 740 filename
  ```

### **Changing Permissions on `demofile.sh`**
To apply specific permissions to a file (`demofile.sh`):
```bash
chmod 710 demofile.sh
```
This grants:
- **Owner**: Full control (rwx)
- **Group**: Execute permission (x)
- **Others**: No permission

---

## **Windows NTFS Permissions**

### **Viewing NTFS Permissions**

To view the current permissions on a file:
```powershell
icacls .\filename
```

### **Granting and Denying Permissions**

- **Grant Full Control to user `dylan`:**
  ```powershell
  icacls .\filename /grant dylan:F
  ```

- **Deny Read permission to `dylan`:**
  ```powershell
  icacls .\filename /deny dylan:R
  ```

- **Remove permissions for user `dylan`:**
  ```powershell
  icacls .\filename /remove:g dylan
  ```

---

## **Windows Share Permissions**

### **Creating a New Share**

To create a new network share:
```powershell
New-SmbShare -Name "LABFILES" -Path "C:\LABFILES" -Description "Share for LABFILES"
```

### **Viewing Shares**

To view all network shares:
```powershell
Get-SMBShare
```

### **View Share Permissions**

To view the permissions on a specific share:
```powershell
Get-SmbShareAccess -Name "LABFILES"
```

### **Granting Permissions on a Share**

To grant the **Change** permission to user `dylan`:
```powershell
Grant-SmbShareAccess -Name "LABFILES" -AccountName "dylan" -AccessRight Change
```

### **Removing Share Permissions**

To remove permissions for user `dylan` on the `LABFILES` share:
```powershell
Revoke-SmbShareAccess -Name "LABFILES" -AccountName "dylan"
```

---

## **Understanding Effective Permissions**

### **Effective Access**

Effective Access combines all **directly assigned** and **inherited** permissions. To view the effective permissions for a user:

1. **Navigate to the file/folder in File Explorer**.
2. **Right-click the file/folder** and select **Properties**.
3. Go to the **Security** tab and select **Advanced**.
4. Click on the **Effective Access** tab, select **Select a user**, and enter the username (e.g., `dylan`).
5. Click **View effective access**.

### **Key Points**
- The **most restrictive** permissions apply (e.g., if a user has Read permission from one source and Deny permission from another, Deny takes precedence).
- **Effective Access** shows what permissions a user will have on a file or folder based on their group memberships and direct permissions.

---

## **Conclusion**

- **Linux**: Use `chmod` and `ls -l` to manage file permissions for users and groups.
- **Windows**: Use **icacls** to manage NTFS file permissions and **SmbShare** cmdlets to manage share permissions.
- Both operating systems use a **combination of direct and inherited permissions**, so always check the **effective access** for troubleshooting.
---