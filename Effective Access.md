# Effective Access

This lab focuses on **Effective Access** in Windows, which is a crucial tool for understanding **accumulated permissions** from direct assignments and group inheritance. Let me guide you step by step. 

---

### **Step-by-Step Instructions:**

1. **Open File Explorer**  
   - Press **Win + E** or type **File Explorer** in the taskbar search and select it.  

2. **Navigate to the File**  
   - In the left pane, expand **This PC** and select **Local Disk (C:)**.  
   - Open the **LABFILES** folder and locate the `comptia-logo` file.  

3. **View File Properties**  
   - Right-click on `comptia-logo` and choose **Properties**.  
   - Go to the **Security** tab.  
   - This tab shows the current NTFS permissions for the file. These might be inherited from the parent folder.

4. **Open Advanced Security Settings**  
   - Click **Advanced**.  
   - In the **Advanced Security Settings** window, go to the **Effective Access** tab.  

5. **Check Effective Access for a User**  
   - Next to **User/Group**, click **Select a user**.  
   - In the **Enter the object name to select** field, type `dylan` and click **OK**.  
   - You’ll be returned to the **Advanced Security Settings** window, with the **User/Group** field set to Dylan (`Dylan@structureality.com`).

6. **View Effective Access**  
   - Click **View effective access**.  
   - Scroll down to see Dylan’s current **effective permissions** for the `comptia-logo` file.  

   **Notice:**  
   - Dylan **does not have** Full control, Change permissions, or Take ownership.  
   - This indicates that Dylan is **not a member of the Power Users group**, which would grant those permissions.

---

### **Understanding Effective Access**  
- **Effective Access** combines all permissions granted directly and inherited from group memberships.  
- It provides a **predictive view**—it does not modify the actual permissions or group memberships.  
- Effective Access also considers **share permissions** if the file is accessible via a shared folder.

**Example:**  
If Dylan is denied **read permission** directly but granted **read permission** through a group, the **denied permission takes precedence**.

---

### **Closing Steps:**  
1. Click **OK** twice to return to File Explorer.  
2. Close File Explorer.

---

### **Why This is Important**  
Effective Access is useful for troubleshooting **access issues** and verifying permissions for security audits. It ensures that no unauthorized user has excessive permissions, which is crucial for security.

---