---
title: "File Permissions"
description: "Understand Linux file permissions: read (r), write (w), execute (x). Learn to change permissions with chmod and ownership with chown."
---

Every file has permissions that control who can read, write, or execute it.

=== "Learn"

    ## View permissions

    When we learned `ls` we saw that by using `-l` to show more information about files. One of those pieces of information is permissions.

    ```bash
    ls -l file.txt
    # drwxr-x--- alice staff Documents/
    # -rw-r--r-- bob staff README.md
    ```

    ### What each letter means

    | Letter | Permission | What it allows |
    | :--- | :--- | :--- |
    | `r` | Read | View file contents / list directory |
    | `w` | Write | Edit file / create or delete files in directory |
    | `x` | Execute | Run file as program / enter directory |
    | `-` | No permission | Access denied |

    ### What each position means

    | Position | What it means | Values |
    | :--- | :--- | :--- |
    | 1 | File type | `-` = file, `d` = directory |
    | 2-4 | Owner permissions | `r`, `w`, `x`, or `-` |
    | 5-7 | Group permissions | `r`, `w`, `x`, or `-` |
    | 8-10 | Others permissions | `r`, `w`, `x`, or `-` |

    So if you take `drwxr-x---` from alice `Documents/` directory:

    ```text
    File  Owner  Group  Others

     d     rwx    r-x    ---
     1     2-4    5-7    8-10
    ```

    - `d` - It's a **directory**
    - `rwx` - Owner (alice) can **Read, Write, Execute**
    - `r-x` - Group (people in staff group) can **Read, Execute** (but not write)
    - *`---` - Others (people not in staff group) have **no access at all**

    ---

    ## Change permissions with `chmod`

    There are two ways to change mode (file permissions)

    ### Symbolic mode

    This mode has letters associated with the position.
    Atfer the letter you put `+` to add or `-` to remove permissions followed by the permissions.

    ```bash
    chmod u+x script.sh    # add execute for owner
    chmod go-w file.txt    # remove write for group and others
    chmod a+r file.txt     # add read for everyone
    ```

    | Symbol | `u` | `g` | `o` | `a` | `+` | `-` | `=` |
    | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
    | Meaning | user / owner | group | others | all (u+g+o) | add | remove | set exactly |

    ### Numeric mode

    ```bash
    chmod 755 script.sh    # owner: rwx, group: r-x, others: r-x
    chmod 600 secret.txt   # owner: rw-, group: ---, others: ---
    ```

    ### Numeric shortcut (octal)

    Each permission has a number: `r=4`, `w=2`, `x=1`. Add them up.

    | Code   | 7     | 6     | 5     | 4     | 0     |
    | :---:  | :---: | :---: | :---: | :---: | :---: |
    | Result | `rwx` | `rw-` | `r-x` | `r--` | `---` |

    ---

    ## Change owner and group with `chown`

    Only `root` or `sudo` can change ownership. `chown` = change ownership

    ```bash
    sudo chown alice file.txt           # change owner to alice
    sudo chown alice:staff file.txt     # change owner AND group
    sudo chown :staff file.txt          # change only group
    ```

    ---

    ## Default permissions: `umask`

    When you create a new file or folder, it gets default permissions.
    `umask` controls what those defaults are.

    ```bash
    umask # shows current value (usually 0022 or 0002)
    ```

    | umask | Files become | Folders become |
    | :--- | :--- | :--- |
    | `022` | `644` - `rw-r--r--` | `755` - `rwxr-xr-x` |
    | `077` | `600` - `rw-------` | `700` - `rwx------` |

    > You probably won't change `umask`. Just know it exists.

=== "Cheat Sheet"

    | Command | What it does |
    | :--- | :--- |
    | `ls -l` | Show permissions, owner, group, size, and date |
    | `chmod 755 file` | Owner rwx, group r-x, others r-x |
    | `chmod u+x file` | Add execute for owner |
    | `chmod go-w file` | Remove write from group and others |
    | `chmod a+r file` | Add read for everyone |
    | `sudo chown alice file` | Change file owner |
    | `sudo chown alice:staff file` | Change owner and group |
    | `umask` | Show default file creation permissions |

=== "Test your knowledge"

    ## Check Your Understanding

    ### 1. Permission code

    What permissions does `chmod 644 file.txt` give to owner, group, and others?

    ??? question "Reveal Answer"
        Owner: `rw-`, Group: `r--`, Others: `r--`

    ### 2. Owner execute

    You want the owner to run `script.sh`, but not give anyone else execute permission.

    **What command do you type?**

    ??? question "Reveal Answer"
        `chmod u+x script.sh`

    ### 3. Change group

    You want `file.txt` to belong to group `staff`.

    **What command do you type?**

    ??? question "Reveal Answer"
        `sudo chown :staff file.txt`

    ### 4. Default permissions

    Which command shows your current umask?

    ??? question "Reveal Answer"
        `umask`
