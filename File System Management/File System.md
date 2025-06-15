# File System

A **file system** is the part of the operating system that manages how data is stored and retrieved on storage devices like hard disks, SSDs, and flash drives.

It provides an abstraction over raw hardware and allows users and programs to:
- Create, name, access, modify, and delete files
- Organize data into directories
- Control permissions and storage allocation

---

## What is a File?

A **file** is a named collection of related data stored on secondary storage.

### Common File Attributes:
| Attribute     | Description                            |
|---------------|----------------------------------------|
| Name          | Human-readable identifier              |
| Type          | E.g., .txt, .exe, .jpg                 |
| Size          | Number of bytes                        |
| Permissions   | Read/write/execute access              |
| Location      | Starting block on disk                 |
| Timestamps    | Created, modified, accessed times      |

---

## File Operations

File systems support basic operations like:

- Create
- Open
- Read
- Write
- Append
- Rename
- Delete
- Seek (move file pointer)
- Close

---

## Directory Structure

A **directory** is a special file that contains a list of file names and metadata.

### Common Directory Organization Methods:
| Type           | Description |
|----------------|-------------|
| Single-Level   | All files in one directory |
| Two-Level      | Separate directory for each user |
| Tree Structure | Hierarchical (e.g., Linux, Windows) |
| Acyclic Graph  | Allows shared files/folders via links |

---

## Storage Allocation Methods

To manage how files are physically placed on disk:

### 1. **Contiguous Allocation**
- Files are stored in consecutive blocks.
- ✅ Fast access  
- ❌ External fragmentation

### 2. **Linked Allocation**
- Each block contains a pointer to the next.
- ✅ No external fragmentation  
- ❌ Slow for random access

### 3. **Indexed Allocation**
- An index block contains pointers to all file blocks.
- ✅ Efficient random access  
- ❌ Overhead of index blocks

---

## Free Space Management

The OS must track available space on disk.

### Methods:
- **Bitmap**: Each block is 0 (free) or 1 (used)
- **Linked List** of free blocks
- **Grouping**: Store addresses of free blocks in groups

---

## File System Mounting

- A **file system** can be mounted (attached) at a specific location in the directory tree.
- Example: Mounting a USB drive at `/media/usb`

---

## Real-World File Systems

| File System | Used In     | Notes                        |
|-------------|-------------|------------------------------|
| FAT32       | Windows     | Legacy, wide compatibility   |
| NTFS        | Windows     | Journaling, permissions      |
| ext4        | Linux       | Default for most distros     |
| APFS        | macOS       | Modern Apple FS              |
| F2FS        | Android     | Flash-optimized FS           |

---

# Summary

- File systems manage **file storage, organization, and access**
- They abstract away **disk structure** and provide a clean interface
- Support both **user-level** operations and **low-level** storage allocation
- Common goals: reliability, speed, space efficiency, and protection
