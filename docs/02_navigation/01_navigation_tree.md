---
title: "Linux Navigation Tree"
description: "Understand the Linux filesystem structure: root (/), home directories, and special paths like ., .., ~, and /. Learn where everything lives."
---

Before you can navigate, you need to know **where you are**.

=== "Learn"

    ## Your Prompt

    Let's check what it means:

    ```text
    username@hostname:~$ [you type here]
    ```

    | Part                  | Example  | Meaning                                   |
    | :-------------------- | :------- | :---------------------------------------- |
    | **Username**          | `bob`    | Who you are                               |
    | **Hostname**          | `laptop` | Which computer                            |
    | **Current directory** | `~`      | Where you are `~` = `/home/your-username` |
    | **Prompt symbol**     | `$`      | Ready for a command                       |

    !!! info "Directory = Folder"

        Same thing. Terminal people say "directory." UI people say "folder." Both mean a place to store files.

    ### `tree` - See the filesystem visually

    `tree` shows your directories as a visual tree

    ```bash
    tree   # check if you have tree in your system
    ```

    ### Common Options

    | Option | What it does |
    | :--- | :--- |
    | `-L 2` | Limit to 2 levels deep |
    | `-d` | Show directories only (no files) |
    | `-a` | Show hidden files |

    ## Navigation Tree

    Everything in Linux starts from **the root** `/`

    Linux treats **everything** as a file. _For example, a directory is just a file that contains a list of other files._

    ### Simplified

    ```text
          / (root)
              │
        ┌─────┴─────┬─────────┐
        │           │         │
      /home       /etc      more...
    (users)   (settings)
        │
      ┌─┴─────┐
      │       │
    diogo    bob → You start here at ~ or /home/your-username
      │
      ├─────────┬─────────┬─────────┐
      │         │         │         │
    Documents Downloads Desktop  more...
    ```

    ### In-depth

    !!! quote "Optional Information"
        You don't need to know this as a beginner but it does not hurt to take a brief look.

    ```
    /
    ├── home/
    │   └── your-username/              ← ~ (your home directory)
    │       ├── Documents/
    │       ├── Downloads/
    │       ├── Desktop/
    │       ├── Pictures/
    │       ├── Music/
    │       └── Videos/
    │
    ├── boot/                   ← Files needed to start Linux
    ├── etc/                    ← System configuration files
    ├── var/                    ← Variable data (logs, caches)
    │   └── log/                ← Log files (for debugging)
    │
    ├── usr/                    ← User programs and files
    │   ├── bin/                ← Most commands (ls, cd, pwd)
    │   ├── lib/                ← Shared libraries
    │   └── local/              ← Programs you install manually
    │
    ├── tmp/                    ← Temporary files (deleted on restart)
    ├── dev/                    ← Device files (USB, drives, etc.)
    ├── mnt/                    ← Temporary mount point
    ├── media/                  ← Removable media (USB, DVD)
    │
    ├── proc/                   ← Running processes (virtual)
    ├── sys/                    ← System information (virtual)
    ├── run/                    ← Runtime data (since last boot)
    └── srv/                    ← Service data (web servers, etc.)
    ```

    > 90% of your time will be spent in /home/your-username/ and its subdirectories.

=== "Cheat Sheet"

    | Command | Options          | What it does                                                         |
    | :---    | :---             | :---                                                                 |
    | `tree`  | `-L`, `-d`, `-a` | Show filesystem as a tree (depth limit, directories only, all files) |

    | Path        | What it means                             |
    | :---        | :---                                      |
    | `/`         | Root directory (everything starts here)   |
    | `~`         | Your home directory `/home/your-username` |
    | `/home/`    | Where all user directories live           |
    | `/etc/`     | System configuration                      |
    | `/var/log/` | Log files                                 |
    | `/usr/bin/` | Most commands - `ls`, `cd`, etc.          |
    | `/tmp/`     | Temporary files (cleared on reboot)       |

=== "Test your knowledge"

    ## Check Your Understanding

    Test yourself on these tree concepts in Linux.

    ### 1. The `~` Symbol

    You see `your-username@laptop:~$` in your prompt.

    What does the `~` symbol represent?

    ??? question "Reveal Answer"
        Your home directory: `/home/your-username`

    ### 2. The `/` Symbol

    You're trying to understand where Linux begins.

    What is `/`?

    ??? question "Reveal Answer"
        The root directory - everything in Linux starts here

    ### 3. Where Commands Live

    You're curious where programs like `ls` and `cd` are stored on disk.

    Where do most Linux commands live?

    ??? question "Reveal Answer"
        `/usr/bin/`

    ###  4. Most of Your Time

    A friend tells you: "90% of your time will be in one place."

    Where will you spend most of your time?

    ??? question "Reveal Answer"
        `/home/your-username/` - your home directory, `~`

    ### 5. See the Tree

    You are no `~` and want to explore your filesystem visually, but only 2 levels deep.

    **What command do you type?**

    ??? question "Reveal Answer"
        `tree -L 2 `
