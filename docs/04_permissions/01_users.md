---
title: "Root User & Sudo"
description: "Learn about the root user (Linux administrator) and sudo. Understand why normal users can't access everything and how to run commands with privileges."
---

In Linux, not all users are equal. Some have more power than others.

=== "Learn"

    `root` is the system administrator - User ID: `0`

    | What | Details |
    | :--- | :--- |
    | **Home folder** | `/root` (not `/home/root`) |
    | **Power** | No limits, no permission checks |
    | **Danger** | Can delete the entire system |

    **With root you can:**

    - Edit/delete any file
    - Install/remove software
    - Create/delete users
    - Change any permission

    > **Why you never log in as root:** Older Linux systems required logging in as `root`. One mistake could destroy everything. Modern Linux locks the `root` account and uses `sudo` instead.

    ## Your User Account

    When you installed Linux, you created a user (e.g., `/home/your-username`).

    **Your user is NOT root.** You have limited permissions.

    ```bash
    ls /root
    # ls: cannot open directory '/root': Permission denied
    ```

    > You can't even look inside /root - that's the root user's personal home folder.

    ## `sudo` - Superuser DO
    `sudo` lets you run a single command as root.

    ```bash
    sudo ls /root
    # [sudo] password for your-username:
    # (shows files inside /root)
    ```

    - Type your user password (not root's password)
    - Linux remembers you for a few minutes so you don't have to retype `sudo`

    ### Kill sudo timeout

    If you want to forget the cached password immediately:

    ```bash
    sudo -k
    ```

    Now the next sudo will ask for password again.

    ## Check who you are

    ```bash
    whoami        # your-username
    sudo whoami   # root (sudo changes who you are temporarily)
    ```

    ```bash
    id            # your user ID (UID) and groups (GID)
    sudo id       # root's user ID (UID=0)
    ```

=== "Cheat Sheet"

    | Command | What it does |
    | :--- | :--- |
    | `sudo <command>` | Run command as root |
    | `sudo -k` | Forget cached sudo password |
    | `whoami` | Show current user |
    | `id` | Show user ID and groups |

=== "Test your knowledge"

    ## Check Your Understanding

    ### 1. Who is root?

    What is the root user in Linux?

    ??? question "Reveal Answer"
        The root user is the system administrator with user ID 0. It can do anything - no limits, no permission checks.

    ### 2. Why not log in as root?

    Why do modern Linux systems lock the root account and use `sudo` instead?

    ??? question "Reveal Answer"
        One mistake as root can destroy the entire system. Using `sudo` limits damage to a single command.

    ### 3. What does `sudo` do?

    You try to look inside `/root` but get "Permission denied".

    **What command do you type to view the contents of `/root`?**

    ??? question "Reveal Answer"
        `sudo ls /root`

    ### 4. sudo timeout

    You just used `sudo`. Now you want to make sure the next `sudo` asks for your password again.

    **What command do you type?**

    ??? question "Reveal Answer"
        `sudo -k` (kills the cached password)

    ### 5. Root Location

    Where does the root user's home directory live?

    ??? question "Reveal Answer"
        `/root` (not `/home/root`)
