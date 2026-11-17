---
tags:
  - "#command"
created: <% tp.file.creation_date("YYYY-MM-DD HH:mm") %>
updated: <% tp.file.last_modified_date("YYYY-MM-DD HH:mm") %>
---

# Linux Folder Deletion Commands

## 1. Delete an Empty Folder

Use `rmdir` when the directory contains nothing.

```bash
rmdir folder_name
```

### Example

```bash
rmdir myfolder
```

---

## 2. Delete a Folder and Its Contents

Use `rm -r` to recursively delete a folder, including files and subdirectories.

```bash
rm -r folder_name
```

### Example

```bash
rm -r myfolder
```

---

## 3. Force Delete a Folder

Use `rm -rf` to recursively and forcefully delete a folder and everything inside it.

```bash
rm -rf folder_name
```

### Example

```bash
rm -rf myfolder
```

> ⚠️ **Warning:** `rm -rf` permanently deletes the specified files and directories. There is no recycle bin.

---

## 4. Delete a Folder Using an Absolute Path

```bash
rm -rf /path/to/folder
```

### Example

```bash
rm -rf ~/projects/my-project
```

---

## 5. Delete a Protected Folder with `sudo`

If you don't have permission:

```bash
sudo rm -rf /path/to/folder
```

### Example

```bash
sudo rm -rf /opt/myapp
```

> ⚠️ Use `sudo rm -rf` carefully. A wrong path can delete critical system files.

---

## 6. Check the Folder Before Deleting

List the current directory:

```bash
ls -l
```

Check a specific folder:

```bash
ls -la folder_name
```

Check the current location:

```bash
pwd
```

A safer workflow:

```bash
pwd
ls -la
rm -rf folder_name
```

---

## Quick Reference

|Command|Purpose|
|---|---|
|`rmdir folder`|Delete an empty folder|
|`rm -r folder`|Delete folder + contents|
|`rm -rf folder`|Force delete folder + contents|
|`sudo rm -rf folder`|Force delete with root privileges|
|`ls -la folder`|Inspect folder before deletion|
|`pwd`|Show current directory|

## Recommended

For normal development work:

```bash
rm -rf folder_name
```

But **always verify the path first**:

```bash
pwd
ls -la
```