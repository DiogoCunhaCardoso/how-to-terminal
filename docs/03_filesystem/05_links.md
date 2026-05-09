---
title: "Links"
description: "Understand Linux hard links and symbolic links (symlinks). Learn the difference between them, how they work with inodes, and when to use each."
---

A link lets you access the same file from multiple locations. Linux has two types: hard links and symbolic links (symlinks).

=== "Learn"

    ## What is an inode?

    Every file has an **inode** (index node) - a unique number that stores <abbr title="File size, permissions, owner, group, timestamps, and location on disk">metadata</abbr> about the file.

    ```bash
    ls -i filename.txt
    # Output: 12345678 filename.txt
    ```

    | Command           | What it shows            |
    | ----------------- | ------------------------ |
    | `ls -i`           | Show inode numbers       |
    | `stat filename`   | Show detailed inode info |

    > The **filename** is just a human-readable label. Linux tracks files by their inode number.

    ---

    ## Hard Links

    A hard link is another name for the **same file** (same inode).

    ```bash
    ln source.txt link.txt   # source.txt must exist beforehand
    ```

    | Feature                  | What it means                            |
    | ------------------------ | ---------------------------------------- |
    | Same inode               | `ls -i` shows same number                |
    | Delete "source.txt"      | File still exists (link.txt still works) |
    | Cannot cross filesystems | Only works on same disk                  |
    | Cannot link directories  | (except with special permission)         |

    ### Visual

    ```
                      ┌────────────┐
                ┌────>│ source.txt │
                │     └────────────┘
      ┌─────────┴────┐
      │ DATA STORAGE │
      │ Inode: 12345 │
      └─────────┬────┘
                │     ┌──────────┐
                └────>│ link.txt │
                      └──────────┘
    ```

    > Essentially, two doors to the same room.

    ---

    ## Symbolic Links (Symlinks)

    A symlink is a **shortcut** that points to another file (different inode).
    ```bash
    ln -s source.txt symlink.txt
    ```

    | Feature               | What it means                         |
    | --------------------- | ------------------------------------- |
    | Different inode       | `ls -i` shows different number        |
    | Delete source         | Symlink becomes broken (red/flashing) |
    | Can cross filesystems | Works across different disks          |
    | Can link directories  | `ln -s /some/folder link`             |

    ### Visual

    ```
    ┌─────────────┐     ┌──────────────┐     ┌─────────────┐     ┌──────────────┐
    │ symlink.txt │ ──> │  LINK DATA   │ ──> │ source.txt  │ ──> │ DATA STORAGE │
    │ (Shortcut)  │     │ Inode: 67890 │     │  (Target)   │     │ Inode: 12345 │
    └─────────────┘     └──────────────┘     └─────────────┘     └──────────────┘
    ```

    !!! tip "Symlink = Shortcut"

        Like desktop shortcuts on Windows/macOS. It's a pointer to the real file.
    ---

    | If you want...                    | Use       |
    | --------------------------------- | --------- |
    | Backup that survives the original | Hard link |
    | Link to a directory               | Symlink   |
    | Link across drives                | Symlink   |
    | Shortcut for a long path          | Symlink   |

    ---

    ### Why a folder always starts with 2 links

      Every folder has at least 2 hard links:

      - The name itself - entry in the parent directory

      - `.` (dot) - points to itself

    ```
        Parent Directory
          │
          │ (Link 1: The Name)
          ↓
    ┌─────────────┐
    │  YourFolder │ <────┐
    └─────────────┘      │ (Link 2: The ".")
          │              │
          └──────────────┘
    ```

    When a subfolder is created it now has 3 links because of `..`.

    ```
    /home/your-user
           │
           ↓
    ┌─────────────┐
    │   folder    │ (3 Links: .  ..  folder (the name))
    └──────┬──────┘
           │  ↑
           │  │ (Link 3: The "..")
           ↓  │
    ┌─────────────┐
    │ sub_folder  │
    └─────────────┘
    ```

    ### `pwd` with symlinks

    | Command           | What it does                                       |
    | :---              | :---                                               |
    | `pwd -L` or `pwd` | Shows the symlink path (Logical - default)         |
    | `pwd -P`          | Shows the real path (Physical - resolves symlinks) |

    ```bash
    pwd -L   # /tmp/link (shows the shortcut)
    pwd -P   # /home/username/real/folder (shows the real destination)
    ```

=== "Cheat Sheet"

    | Command | What it does |
    | :---                | :---                                           |
    | `ln source link`    | Create hard link                               |
    | `ln -s source link` | Create symbolic link                           |
    | `ls -i`             | Show inode numbers                             |
    | `stat <file>`       | Show detailed inode info                       |
    | `pwd -L`            | Show logical path (follows symlinks - default) |
    | `pwd -P`            | Show physical path (resolves symlinks)         |

=== "Test your knowledge"

    ## Check Your Understanding

    ### 1. Hard link vs Symlink

    You delete `source.txt`. Which link still works?

    ??? question "Reveal Answer"
        The hard link. It shares the same inode, so the data remains.
        A symlink becomes broken.

    ### 2. Cross-filesystem links

    You want to link a file from your SSD to a USB drive.

    **Can both hard links and symlinks do this?**

    ??? question "Reveal Answer"
        Only symlinks. Hard links cannot cross filesystems.

    ### 3. Link to a directory

    You want to create a shortcut to `/home/your-username/my-photos/animals/cute-cat.png`.

    **What command do you use?**

    ??? question "Reveal Answer"
        `ln -s /home/your-username/my-photos/animals/cute-cat.png cat_photo`

    ### 4. Finding the real path

    You're inside a symlinked directory and `pwd` shows the shortcut path.

    **How do you see the real (physical) path?**

    ??? question "Reveal Answer"
        `pwd -P` (Physical path, resolves symlinks)

    ### 5. Folder link count

    A new empty folder has a link count of 2. What are they?

    ??? question "Reveal Answer"
        1. The folder name (entry in parent directory)
        2. `.` (dot - points to itself)

    ### 6. What happens to a symlink when you move the target?

    You have `symlink.txt` pointing to `source.txt`. You move `source.txt` to a different folder.

    **Does `symlink.txt` still work?**

    ??? question "Reveal Answer"
        No. The symlink becomes broken. Symlinks store the path, not the inode.
