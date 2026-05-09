---
title: "User Management"
description: "Learn how to add, remove, and manage users in Linux. Understand adduser vs useradd, service accounts, and where user information is stored."
---

Adding users requires `sudo` - only root can create new users.

=== "Learn"

    ## `adduser` - Add users step by step

    `adduser` is interactive. It asks questions and sets things up automatically.

    ```bash
    sudo adduser alice # new user named alice
    ```

    - Prompts for a password for `alice` (UNIX password)

    - Asks for full name, room number, work phone, home phone, other (press Enter to skip)

    - Confirms info with Y - Linux creates default files and UserID (UID) automatically.

    ```bash
    ls /home
    # alice  diogo  (new user's home folder appears)
    ls -la /home/alice
    # .bashrc  .profile  (default files)
    ```

    ---

    ## Change password

    ### Another user's password

    ```bash
    sudo passwd alice
    ```
    You'll be asked for:

    - New password for Alice
    - Confirm new password

    > You're an admin. You don't need to know the old password to change it.

    ### Your own password

    ```bash
    passwd # no sudo required
    ```

    You'll be asked for:

    - Your current password
    - New password
    - Confirm new password

    ---

    ## Delete a user

    ```bash
    sudo userdel alice      # deletes user, keeps /home/alice
    sudo userdel -r alice   # deletes user AND /home/alice
    ```

    ### Why keep the home folder?

    | Scenario | What you want                                                                                                            |
    | :---     | :---                                                                                                                     |
    | Alice left the company. She shouldn't be able to log in anymore, but her files might be needed later | Keep `/home/alice` (no `-r`) |
    | Alice was a temporary test account. You'll never need anything from it or you need disk space | Delete everything (`-r`) |

    > `userdel` without `-r` removes Alice's **access** (password, login ability) but keeps **her files**. You can delete the folder later with `rm -rf /home/alice` if you decide you don't need them.

    !!! tip "Forgot `sudo`? Use `sudo !!`"

        You type a command that needs `sudo`, but forgot sudo:

        ```bash
        passwd alice   # Permission Denied
        sudo !!        # Works!
        ```
    > `!!` retrieves the last written command, though it is commonly used with sudo.

    ---

    ## Where user info is stored

    !!! quote "Optional deep dive."
         You don't need it to use Linux, but it helps understand how user info is organized.

    | File | What it stores |
    | :--- | :--- |
    | `/etc/passwd` | Username, UID, home folder, shell |
    | `/etc/shadow` | Encrypted password |
    | `/etc/group` | Which groups users belong to |

    > Don't edit these files directly. Use `adduser`, `passwd`, `userdel` instead.

    ### `/etc/passwd` explained

    View all users on the system:

    ```bash
    cat /etc/passwd
    ```

    Each line represents an account (users & system/service accounts). Example lines:

    ```bash
    root:x:0:0:root:/root:/bin/bash
    your-username:x:1000:1000:Real Name:/home/your-username:/bin/bash
    ```

    Fields are separated by a `:` (colon)

    ```text
    your-username:x:1000:1000:Real Name:/home/your-username:/bin/bash
            │     │   │    │       │               │            │
            │     │   │    │       │               │            └── Shell (bash)
            │     │   │    │       │               │
            │     │   │    │       │               └── Home directory
            │     │   │    │       │
            │     │   │    │       └── Full name (GECOS)
            │     │   │    │
            │     │   │    └── Group ID (GID)
            │     │   │
            │     │   └── User ID (UID)
            │     │       (first regular user starts at 1000)
            │     │
            │     └── Password placeholder
            │         (x means in /etc/shadow)
            │
            └── Username
    ```

    > If you add the username, room, work phone, home phone, and other information, that information will appear here after groupID separated by `,` (comma)

    ### `/etc/shadow` explained

    This file stores encrypted passwords. Only `root` can read it.

    ```bash
    sudo cat /etc/shadow
    ```

    Each line represents an account. Example lines:

    ```bash
    root:$6$randomhash...:19120:0:99999:7:::
    your-username:$6$differenthash...:19120:0:99999:7:::
    daemon:*:19120:0:99999:7:::
    ```

    Fields are separated by a `:` (colon)

    ```text
    your-username:$6$differenthash...:19120:0:99999:7:::
           │      │                     │   │   │   │
           │      │                     │   │   │   └── Warn 7 days before expiration
           │      │                     │   │   │
           │      │                     │   │   └── Max: 99999 days (never expires)
           │      │                     │   │
           │      │                     │   └── Min: 0 days (can change anytime)
           │      │                     │
           │      │                     └── Last changed: 19120 days since Jan 1, 1970
           │      │
           │      └── $6$ (SHA-512) + Salt + Encrypted hash
           │
           └── Username
    ```

    > Service accounts have `*` or `!` instead of a password. You can't log into them.

    ### `/etc/group` explained

    This file stores group information. Groups let you manage permissions for multiple users at once.

    ```bash
    cat /etc/group
    ```

    Each line represents one group. Example lines:

    ```bash
    root:x:0:
    sudo:x:27:alice,bob
    developers:x:1001:alice
    your-username:x:1000:
    ```

    Fields are separated by a `:` (colon)

    ```text
    developers:x:1001:your-username,alice
         │     │  │          │
         │     │  │          └── Members (users in this group, comma-separated)
         │     │  │
         │     │  └── Group ID (GID)
         │     │
         │     └── Password placeholder (x means in /etc/gshadow)
         │
         └── Group name
    ```

=== "Cheat Sheet"

    | Command | What it does |
    | :--- | :--- |
    | `sudo adduser <name>` | Add new user (interactive) |
    | `sudo passwd <user>` | Change another user's password |
    | `passwd` | Change your own password |
    | `sudo userdel <user>` | Delete user (keep home folder) |
    | `sudo userdel -r <user>` | Delete user AND home folder |
    | `sudo !!` | Re-run last command with sudo |

=== "Test your knowledge"

    ## Check Your Understanding

    ### 1. Add a new user

    You want to create a new user named `john`.

    **What command do you type?**

    ??? question "Reveal Answer"
        `sudo adduser john`

    ### 2. Change another user's password

    Alice forgot her password. You need to set a new one for her.

    **What command do you type?**

    ??? question "Reveal Answer"
        `sudo passwd alice`

    ### 3. Change your own password

    **What command do you type?**

    ??? question "Reveal Answer"
        `passwd` (no sudo needed)

    ### 4. Delete a user (keep files)

    Alice left the company. She shouldn't log in anymore, but her files might be needed later.

    **What command do you type?**

    ??? question "Reveal Answer"
        `sudo userdel alice` (keeps `/home/alice`)

    ### 5. Delete user AND home folder

    Bob was a temporary test account. You need the disk space back.

    **What command do you type?**

    ??? question "Reveal Answer"
        `sudo userdel -r bob`

    ### 6. Forgot sudo

    You typed `passwd alice` and got "Permission denied".

    **What's the fastest way to re-run it with sudo?**

    ??? question "Reveal Answer"
        `sudo !!`

    ### 7. Where is password stored?

    Which file stores encrypted passwords (only readable by root)?

    ??? question "Reveal Answer"
        `/etc/shadow`

    ### 8. Service account indicator

    You see `daemon:*:...` in `/etc/shadow`. What does `*` mean?

    ??? question "Reveal Answer"
        The account cannot log in (service account)
