---
title: "Searching"
description: "Learn how to find files and search for text within files using find, grep, and pipes. Master filtering command outputs and time-based searches."
---

You can create and view files. Now let's learn how to **find them**, **search inside them**, and **filter terminal outputs** using pipes.

=== "Learn"

    ## `find` - Search for files and directories

    The `find` command searches the filesystem for files and directories based on names, size, permissions, and even time.

    ```bash
    find . -name "notes.txt"   # find "notes.txt" in current directory and subfolders
    ```

    ### Searching by Name & Type

    - `-name`: Case-sensitive search.
    - `-iname`: Case-insensitive (ignores if it's uppercase or lowercase).
    - `-type f` (files) or `-type d` (directories).

    ```bash
    find /home -iname "*.jpg"     # case-insensitive search in /home
    find . -type d -name "src"    # find only directories named "src"
    find . -maxdepth 1 -name "*"  # search only in the current folder, no subfolders
    ```

    > Pros: Extremely powerful filtering. Cons: Syntax can be tricky for complex searches.

    ### Searching by Time (Advanced)

    Find files based on when they were last touched.

    | Option | Unit | Meaning |
    | :--- | :--- | :--- |
    | `-mtime` | Days | Content was modified |
    | `-mmin`  | Minutes | Content was modified |
    | `-atime` | Days | File was accessed (read) |
    | `-ctime` | Days | Metadata changed (permissions/owner) |

    ```bash
    find . -mmin -60          # Modified in the last hour
    find . -mtime -7          # Modified in the last 7 days
    find . -mtime +3 -and -mtime -7 # Modified between 3 and 7 days ago
    ```

    ### Permissions and Ownership

    You can also find files based on who owns them or what they are allowed to do:

    ```bash
    sudo find /srv/chemistry/ -user ryan    # Files owned by user "ryan"
    sudo find /srv/chemistry/ -group lisa   # Files belonging to group "lisa"
    find . -perm 777                        # Files with full read/write/execute permissions
    ```

    ---

    ## `grep` - Search for text inside files

    While `find` looks for the file itself, `grep` looks at what is **inside** the file.

    ```bash
    grep "error" log.txt   # prints lines containing "error"
    ```

    ### Useful options

    | Option | What it does | Example |
    | :--- | :--- | :--- |
    | `-i` | Ignore case | `grep -i "critical" app.log` |
    | `-r` | Search recursively | `grep -r "TODO" ./projects` |
    | `-n` | Show line numbers | `grep -n "main" script.py` |
    | `-v` | Invert match (hide lines) | `grep -v "info" debug.log` |

    ```bash
    grep -rn "API_KEY" .   # search recursively showing line numbers
    ```

    ---

    ## `|` (Pipes) - Filtering Command Output

    The third core concept of searching is using the pipe (`|`) to send the output of *any* command directly into `grep`. This allows you to search through live system data, command histories, or process lists instead of static files.

    ```bash
    history | grep "sudo"  # search your command history for "sudo"
    ```

    ### How it works:
    The standard output (**stdout**) of the command on the left becomes the standard input (**stdin**) of the command on the right.

    ```bash
    ls -la | grep "Dec"    # show only files modified in December
    ps aux | grep "python" # search active system processes for "python"
    ```

    !!! tip "Chaining Filters"
        You can chain multiple pipes together to narrow down your search:
        ```bash
        history | grep "git" | grep -v "commit" # find git commands, but hide commits
        ```

=== "Cheat Sheet"

    | Command / Flags | What it does | Example |
    | :--- | :--- | :--- |
    | `find . -name [name]` | Find by name (case-sensitive) | `find . -name "app.log"` |
    | `find . -iname [name]` | Find by name (case-insensitive) | `find . -iname "readme.md"` |
    | `find . -type f / d` | Filter by file or directory | `find . -type d -name "src"` |
    | `find . -mmin -N` | Modified in the last N minutes | `find . -mmin -10` |
    | `find . -mtime -N` | Modified in the last N days | `find . -mtime -7` |
    | `find . -perm [mode]` | Search by file permissions | `find . -perm 777` |
    | `grep [text] [file]` | Search text inside a file | `grep "error" production.log` |
    | `grep -r [text] [dir]` | Search text recursively in directory | `grep -r "DATABASE_URL" .` |
    | `grep -i` | Ignore case during text search | `grep -i "critical" app.log` |
    | `grep -v` | Invert match (hide matching lines) | `grep -v "DEBUG" server.log` |
    | `[command] \| grep [text]` | Pipe output to filter results with grep | `history \| grep "ssh"` |

    > Use `-and`, `-not` (or `!`) to build complex search queries with `find`.

=== "Test your knowledge"

    ## Check Your Understanding

    Test yourself with these real terminal scenarios.

    ### 1. The Quick Fix

    You just edited a configuration file 5 minutes ago but forgot which one it was in a sea of folders.

    **What command shows files modified in the last 10 minutes?**

    ??? question "Reveal Answer"

        ```bash
        find . -mmin -10
        ```

    ---

    ### 2. Deep Project Search

    You need to find where a specific environment variable named `STRIPE_SECRET` is defined inside a large multi-folder project. You need to know the exact file and line number.

    **What command do you type?**

    ??? question "Reveal Answer"

        ```bash
        grep -rn "STRIPE_SECRET" .
        ```
        The `-r` searches recursively through all subfolders, and `-n` prints the line numbers.

    ---

    ### 3. Security Audit

    You need to find all directories in your current folder that have unsafe `777` permissions to make sure your workspace is secure.

    **What command do you type?**

    ??? question "Reveal Answer"

        ```bash
        find . -type d -perm 777
        ```
        `-type d` targets only directories, and `-perm 777` checks for full read, write, and execute permissions.

    ---

    ### 4. Filtering Live Server Logs

    You are debugging an app and want to see if a specific process called "nginx" is currently running on the system using the `ps aux` command.

    **How do you filter the process list using a pipe?**

    ??? question "Reveal Answer"

        ```bash
        ps aux | grep "nginx"
        ```
        This takes the massive list of running processes from `ps aux` and passes it to `grep` to show only lines containing "nginx".

    ---

    ### 5. Smart Cleanup & Logic

    You want to find all `.tmp` files in your project directory that haven't been touched or modified in the last 30 days so you can inspect them.

    **What command do you type?**

    ??? question "Reveal Answer"

        ```bash
        find . -name "*.tmp" -mtime +30
        ```
        Using `+30` tells `find` to look for files modified *more* than 30 days ago.