---
title: "Searching"
description: "Learn how to find files and search for text within files using find, grep, and pipes. Master filtering command outputs and time-based searches."
---

You can create and view files. Now let's learn how to **find them**, **search inside them**, and **filter outputs**.

=== "Learn"

    ## Finding vs. Searching

    Before diving in, understand the difference between the two main tools:

    | Tool | What it looks for | Best used for |
    | :--- | :--- | :--- |
    | **`find`** | File metadata (Names, dates, sizes) | Locating a lost file or directory |
    | **`grep`** | Text content *inside* files | Finding a specific line, variable, or log error |

    ---

    ## `find` - Search for files and directories

    The `find` command searches the filesystem based on names, size, permissions, and even time.

    ```bash
    find . -name "notes.txt"   # find "notes.txt" in current directory and subfolders
    ```

    ### Useful options

    | Option | What it does | Example |
    | :--- | :--- | :--- |
    | `-name` | Search by filename (case-sensitive) | `find . -name "app.log"` |
    | `-iname` | Search by filename (case-insensitive) | `find . -iname "readme.md"` |
    | `-type f` | Search for **f**iles only | `find . -type f` |
    | `-type d` | Search for **d**irectories only | `find . -type d -name "src"` |
    | `-maxdepth` | Limit how deep subfolders are searched | `find . -maxdepth 1 -name "*.sh"` |

    > Pros: Extremely powerful filtering. Cons: Syntax can be tricky for complex searches.

    ### Searching by Time (Advanced)

    You can locate files based on when they were last modified or accessed.

    - `-mmin N`: Content was modified `N` minutes ago.
    - `-mtime N`: Content was modified `N` days ago.

    ```bash
    find . -mmin -60          # Modified in the last hour (less than 60 mins)
    find . -mtime -7          # Modified in the last 7 days
    find . -mtime +3 -and -mtime -7 # Modified between 3 and 7 days ago
    ```

    ### Permissions and Ownership

    ```bash
    sudo find /srv -user ryan    # Files owned by user "ryan"
    find . -perm 777             # Files with unsafe world-writable permissions
    ```

    ---

    ## `grep` - Search for text inside files

    Instead of digging through countless lines manually, `grep` scans the content of files to match text patterns.

    ```bash
    grep "error" log.txt   # prints lines containing "error"
    ```

    ### Common Grep Flags

    | Option | What it does | Example |
    | :--- | :--- | :--- |
    | `-i` | Ignore case (case-insensitive) | `grep -i "critical" app.log` |
    | `-r` | Search recursively in subfolders | `grep -r "TODO" ./projects` |
    | `-n` | Show line numbers of the match | `grep -n "main" script.py` |
    | `-v` | Invert match (hide lines matching text) | `grep -v "info" debug.log` |
    | `-c` | Count the number of matching lines | `grep -c "fox" sample.txt` |
    | `-e` | Protect patterns starting with a hyphen `-` | `grep -e "-v" file.conf` |

    > Without `-e`, running `grep "-v" file.conf` makes grep think you want to use the invert flag. `-e` ensures it's read as plain text.

    ---

    ## `|` - Pipe: Combine commands to filter output

    Just like you saw in Redirection, the pipe `|` takes the stdout of the left command and passes it as stdin to `grep`. This lets you search live terminal outputs.

    ```bash
    history | grep "sudo"  # search your command history for "sudo"
    ```

    ```bash
    ls -la | grep "Dec"    # show only files modified in December
    ps aux | grep "python" # search active system processes for "python"
    ```

    ### Advanced Filtering with Regex
    Using `$` anchors your search to the **end** of a line:

    ```bash
    ls /var/log | grep '.log$'  # list only files ending exactly with .log
    ```

    > You can chain multiple pipes together: `history | grep "git" | grep -v "commit"`

=== "Cheat Sheet"

    | Command | Options | What it does |
    | :--- | :--- | :--- |
    | `find` | `-name` `-iname` | Search by filename (case sensitive/insensitive) |
    | `find` | `-type f` / `-type d` | Filter results by files or directories |
    | `find` | `-mmin -N` / `-mtime -N` | Find files modified in the last N minutes/days |
    | `find` | `-perm [mode]` | Search for files with specific permissions |
    | `grep` | `-i` `-r` | Search text inside files (ignore case / recursive) |
    | `grep` | `-n` `-v` | Show matching line numbers / Hide matching lines |
    | `grep` | `-c` `-e` | Count matches / Protect patterns starting with `-` |
    | `\| grep` | - | Pipe any command output into grep to filter it |

=== "Test your knowledge"

    ## Check Your Understanding

    Test yourself with these real terminal scenarios.

    ### 1. Save a directory listing

    You just edited a configuration file 5 minutes ago but forgot which one it was in a sea of folders.

    **What command shows files modified in the last 10 minutes?**

    ??? question "Reveal Answer"

        ```bash
        find . -mmin -10
        ```

    ### 2. Deep Project Search

    You need to find where a specific environment variable named `STRIPE_SECRET` is defined inside a large multi-folder project. You need to know the exact file and line number.

    **What command do you type?**

    ??? question "Reveal Answer"

        ```bash
        grep -rn "STRIPE_SECRET" .
        ```

    ### 3. Hyphen Pattern Traps

    You want to search a configuration file named `settings.json` for the exact string `--debug`.

    **What command ensures the pattern isn't confused with a flag?**

    ??? question "Reveal Answer"

        ```bash
        grep -e "--debug" settings.json
        ```

    ### 4. Live Server Stats

    Instead of seeing hundreds of log lines containing the word "404", you just want a quick count of how many times a "404" error occurred in `access.log`.

    **What command do you run?**

    ??? question "Reveal Answer"

        ```bash
        grep -c "404" access.log
        ```

    ### 5. Advanced Pipe Filtering

    You are listing a directory using `ls /var/log`, but you only want to see filenames that end precisely with `.log`.

    **How do you filter the output using a pipe and regex?**

    ??? question "Reveal Answer"

        ```bash
        ls /var/log | grep '.log$'
        ```