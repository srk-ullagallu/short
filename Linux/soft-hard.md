# inodes
- In linux to use disks we need to create fs
- When we create any fs in linux it has comes with inodes
- Linux uses the inode datastructure to store the files and directories in disks
- file names are not stored in the inodes directories stores the filename

#### Key Details About Inodes:
- **Metadata Stored in Inode**:
  - File size
  - File permissions (read, write, execute)
  - Ownership (user and group IDs)
  - Timestamps (creation, modification, access)
  - File type (regular file, directory, etc.)
  - Number of hard links
  - Pointers to the file's data blocks on the disk

- **Metadata NOT in Inode**:
  - The filename is **not** stored in the inode. Instead, filenames are stored in the directory entries, which map the name to the inode number.

- **Viewing Inode Information**:
  Use the `ls` command with `-i` to see the inode number of files.
  ```bash
  ls -i
  ```

---

### **2. Soft Link (Symbolic Link):**
A **soft link**, or **symbolic link**, is like a shortcut to another file. It is a separate file that points to the original file by its path.

#### Characteristics of Soft Links:
- It has its own inode number, different from the original file.
- If the original file is deleted, the soft link becomes **broken** and won't work.
- Can link to files or directories, even across different filesystems.
- Creation:
  ```bash
  ln -s <target_file> <soft_link_name>
  ```
- Example:
  ```bash
  ln -s /home/user/file.txt link_to_file
  ```

#### Check Soft Links:
Use `ls -l` to identify soft links. They are denoted by an arrow (`->`).
```bash
ls -l
# Output: link_to_file -> /home/user/file.txt
```

---

### **3. Hard Link:**
A **hard link** is an additional name for an existing file. Both the original file and the hard link share the same inode and data blocks.

#### Characteristics of Hard Links:
- The original file and the hard link are **indistinguishable**.
- Both have the same inode number.
- If the original file is deleted, the hard link still points to the data, so the file is not truly deleted until all hard links are removed.
- Cannot link to directories (for safety reasons).
- Cannot span across different filesystems.

#### Creation:
```bash
ln <target_file> <hard_link_name>
```
- Example:
  ```bash
  ln /home/user/file.txt hard_link_to_file
  ```

#### Check Hard Links:
Use `ls -l` to view the number of links to a file. The link count is shown in the second column.
```bash
ls -l
# Output: -rw-r--r-- 2 user group 1024 Jan 19 12:00 file.txt
```

---

### **Differences Between Soft and Hard Links**:

| Feature              | Soft Link (Symbolic Link) | Hard Link                       |
|----------------------|---------------------------|----------------------------------|
| **Inode**           | Has a different inode.    | Shares the same inode as the original. |
| **Link to Directories** | Yes                     | No                               |
| **Across Filesystems** | Yes                     | No                               |
| **Effect of Original File Deletion** | Becomes broken (invalid). | Still accessible through the link. |
| **Usage**            | Like a shortcut.         | Creates an additional name for the same file. |


----