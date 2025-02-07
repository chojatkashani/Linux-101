# Linux-101

# File Permissions in Linux

## **Project Description**

The research team at my organization needed to **update file permissions** for specific **files and directories** within the `projects` directory. The current permissions did **not align with the required authorization levels**. Checking and updating these permissions was necessary to **enhance system security**.

To complete this task, I performed the following steps:

---

## **Step 1: Checking File and Directory Details**

The following **Linux command** was used to determine the **existing permissions** for files and directories:

```bash
ls -la
```

### **Example Output:**
```
drwxr-xr-x  3 user user 4096 Jan 10 12:00 drafts
-rw-rw-r--  1 user user 1200 Jan 10 12:01 project_t.txt
-rw-rw-r--  1 user user 1300 Jan 10 12:02 project_k.txt
-rw-r--r--  1 user user 1400 Jan 10 12:03 .project_x.txt
```

- The **first column** in the output displays a **10-character string** that represents **file permissions**.
- This listing shows:
  - **A directory (`drafts`)**.
  - **A hidden file (`.project_x.txt`)**.
  - **Multiple project files (`project_t.txt`, `project_k.txt`)**.

---

## **Step 2: Understanding the File Permissions String**

The **10-character string** in the **first column** can be broken down as follows:

| Position | Meaning |
|----------|---------|
| **1st character** | `d` (directory) or `-` (regular file) |
| **2nd-4th** | User permissions (Read `r`, Write `w`, Execute `x`) |
| **5th-7th** | Group permissions (Read `r`, Write `w`, Execute `x`) |
| **8th-10th** | Other permissions (Read `r`, Write `w`, Execute `x`) |

### **Example Analysis: `-rw-rw-r--` (project_t.txt)**
- **`-`** → Regular file (not a directory).
- **`rw-`** → User has **read & write** permissions.
- **`rw-`** → Group has **read & write** permissions.
- **`r--`** → Others have **read-only** permissions.

---

## **Step 3: Changing File Permissions**

### **Removing Write Permissions from "Other" on `project_k.txt`**
The organization **determined that `other` users should not have write access** to any files.

#### **Command Used:**
```bash
chmod o-w project_k.txt
ls -la
```

- The **chmod** command modifies file permissions.
- **`o-w`** removes **write access** from **other**.
- Running **`ls -la`** again **verifies the change**.

---

## **Step 4: Changing Permissions on a Hidden File**

The **research team archived `project_x.txt`** and **no longer wants anyone to have write access** to it.  
However, the **user and group should still have read access**.

#### **Command Used:**
```bash
chmod u-w .project_x.txt
chmod g-w .project_x.txt
chmod g+r .project_x.txt
ls -la
```

- **`chmod u-w`** → Removes **write permission from the user**.
- **`chmod g-w`** → Removes **write permission from the group**.
- **`chmod g+r`** → **Adds read permission to the group**.

---

## **Step 5: Changing Directory Permissions**

The organization decided that **only the `researcher2` user** should have **access to the `drafts` directory**.  
**No one else should have execute (`x`) permissions**.

#### **Command Used:**
```bash
chmod g-x drafts
ls -la
```

- **`chmod g-x drafts`** → Removes **execute permission** from the group.
- **`researcher2`** already had **execute permissions**, so no additional changes were needed.

---

## **Summary**

I successfully updated **file and directory permissions** to **match the organization’s security requirements**:

1. **Checked permissions** using `ls -la`.
2. **Removed unnecessary write permissions** from `project_k.txt`.
3. **Restricted write access** to the hidden file `.project_x.txt`.
4. **Limited access to the `drafts` directory**, ensuring **only `researcher2` could execute** commands.

By **using the `chmod` command**, I ensured **proper access control**, reducing security risks and **protecting sensitive data**.
