# Managing Permissions

Last part for the managing permission on  **Windows share permissions** using **PowerShell**. This exercise focuses on **creating a share**, **viewing permissions**, **granting permissions**, and **removing permissions** for the user `dylan`.

---

### **Step-by-Step Guide:**

1. **Ensure PowerShell is Running as Administrator**  
   - If it’s not already open, run **PowerShell as Administrator**:  
     - Click **Start**, type `PowerShell`, right-click it, and select **Run as Administrator**.  
     - Click **Yes** on the UAC prompt.  

---

### **Create a New Share**  
- Run the following command to create a network share called `LABFILES` pointing to `C:\LABFILES`:  
  ```powershell
  New-SmbShare -Name "LABFILES" -Path "C:\LABFILES" -Description "Share for LABFILES"
  ```

  **Explanation:**  
  - **`-Name "LABFILES"`**: The name of the network share.  
  - **`-Path "C:\LABFILES"`**: Specifies the folder to be shared.  
  - **`-Description "Share for LABFILES"`**: Optional description for the share.  

---

### **View Current Shares**  
- To see all shared folders on the system, run:  
  ```powershell
  Get-SMBShare
  ```
  This command displays a list of all shares, including their names, paths, and descriptions.

---

### **Check Share Permissions**  
- To view the permissions of the `LABFILES` share, run:  
  ```powershell
  Get-SmbShareAccess -Name "LABFILES"
  ```

  **Example Output:**  
  ```
  Name      AccountName      AccessControlType      AccessRight  
  ----      -----------      -----------------      -----------  
  LABFILES  Everyone         Allow                  Full  
  ```

---

### **Grant Change Permission to User Dylan**  
- Run the following command to grant `dylan` **Change** permission on the `LABFILES` share:  
  ```powershell
  Grant-SmbShareAccess -Name "LABFILES" -AccountName "dylan" -AccessRight Change
  ```
- When prompted, type `Y` to confirm.  

**Explanation:**  
- **`-AccessRight Change`**: Grants read and write access but not full control.  
- **`-AccountName "dylan"`**: Specifies the user account for the permission change.  

---

### **Remove Dylan’s Share Permission**  
- To remove `dylan`’s specific permission on the `LABFILES` share, run:  
  ```powershell
  Revoke-SmbShareAccess -Name "LABFILES" -AccountName "dylan"
  ```
- When prompted, type `Y` to confirm.  

---

### **Important Notes on Share vs. NTFS Permissions:**  
- **NTFS permissions** control access to the file system.  
- **Share permissions** control access when files are accessed over the network.  
- **The Most Restrictive Rule Wins:** If share permissions allow Full Control, but NTFS allows only Read, the user will have **Read** access.

---

### **Summary of Commands:**

| Command                                    | Description                           |
|--------------------------------------------|---------------------------------------|
| `New-SmbShare`                             | Create a new share                    |
| `Get-SMBShare`                             | View all shares                       |
| `Get-SmbShareAccess`                       | View permissions for a specific share |
| `Grant-SmbShareAccess`                     | Grant permissions on a share          |
| `Revoke-SmbShareAccess`                    | Remove specific permissions from a share |

---
