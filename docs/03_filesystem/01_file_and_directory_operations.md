---
title: "File & Directory Operations"
description: "Learn how to create, copy, move, and delete files in Linux. Learn mkdir, cp, mv, rm, wildcards, and brace expansion."
---

Let's learn how to **create, copy, move, and delete** files and directories.

=== "Learn"

    ## `mkdir` - Create directories

    `mkdir` stands for **M**a**k**e **Dir**ectory. It creates new directories.

    ```bash
    mkdir my_folder   # creates a folder called "my_folder"
    ```

    ### Nested directories

    ```bash
    mkdir -p projects/2024/reports
    ```

    > Without -p, you'd need: `mkdir projects projects/2024 projects/2024/reports`

    ---

    ## `touch` - Creates files

    `touch` creates an empty file. If the file already exists it updates its timestamp.

    ```bash
    touch my_file_name.txt
    ```

    ---

    ## `cp` - Copy files and directories

    `cp` stands for **C**o**p**y. It duplicates files.

    ```bash
    cp original.txt backup.txt
    ```

    ### Copy directories

    Add `-r` (recursive) to copy folders and everything inside:

    ```bash
    cp -r projects/ projects_backup/
    ```

    !!! tip "Deep paths tip"
        Copying into deep paths is error-prone:

        ```bash
        cp /long/source/path/file.txt /long/destination/nested/path/
        ```

        Instead do this:

        ```bash
        cd /long/destination/nested/path/ # cd to the folder you want to copy into
        cp /long/source/path/file.txt .   # use . to say "right here"
        ```
    ---

    ## `mv` - Move or rename

    `mv` stands for **M**o**v**e. It moves or renames files and directories.

    ```bash
    mv old.txt new.txt                  # rename
    mv file1.txt file2.txt Documents/   # move
    ```

    > No -r needed for folders. Works the same.

    ---

    ## `rm` - Removes files or directories

    `rm` stands for **R**e**m**ove. It deletes permanently. No trash bin. No undo.

    ```bash
    rm useless.txt
    ```

    ### Common Options

    | Option | Meaning            | Why you need it                                  |
    | :----- | :----------------- | :----------------------------------------------- |
    | `-r`   | Recursive          | Delete folders (and everything inside)           |
    | `-f`   | Force              | Skip confirmation prompts - dangerous but useful |
    | `-i`   | Interactive        | Confirm each file before deletion - safe mode    |

    !!! danger "Never run these!"
        ```bash
        rm -rf /   # Deletes your entire system
        rm -rf ~   # Deletes all your personal files
        ```

    ```bash
    rm -i file.txt   # Asks: "rm: remove regular file 'hello.txt'? y/n"
    ```

    ---

    ## `rmdir` - Remove empty directories

    `rmdir` removes **empty** directories only.

    ```bash
    rmdir empty_folder
    rmdir -p parent/child/
    ```

    > Less useful as `rmdir` refuses to delete folders with stuff inside. That's what `rm -r` is for.

    ---

    ## Advanced Commands

    !!! quote "Optional: Wildcards & Brace Expansion"
        These are powerful but you can still get around without knowing them.

    ### Wildcards

    | Wildcard | What it matches | Example |
    | :--- | :--- | :--- |
    | `*` | Anything (zero or more characters) | `rm *.txt` |
    | `?` | Exactly one character | `file?.txt` |
    | `[abc]` | One character from the set | `file[123].txt` |
    | `[a-z]` | One character from the range | `file[a-c].txt` |

    > You can combine wildcards: `*[0-9]*`, `backup*`, `???` - What would these do?

    ??? question "Answers"
        - `*[0-9]*` - any file containing a number (e.g., file1.txt, data2.log, 3notes.md)
        - `backup*` - any file starting with "backup" (e.g., `backup.txt`, `backup_old.zip`)
        - `???` - any file with exactly 3 characters (e.g., `dog`, `123`, `a-b`)

    ### Brace Expansion

    | Pattern | What it generates | Example |
    | :--- | :--- | :--- |
    | `{a,b,c}` | Each item in the list | `touch {README,INSTALL}.md` |
    | `{1..10}` | Sequence of numbers | `mkdir day_{1..7}` |
    | `{a..z}` | Sequence of letters | `touch letter_{a..d}.txt` |

    > You can combine and nest brace expansions. What do these do?
    > - `{a,b}{1,2}`
    > - `notes.txt{,.bak}`
    > - `{src,docs}/{assets,data}`

    ??? question "Answers"
        - `{a,b}{1,2}` → `a1 a2 b1 b2` (cartesian product)
        - `notes.txt{,.bak}` → `notes.txt notes.txt.bak` (backup pattern)
        - `{src,docs}/{assets,data}` → `src/assets src/data docs/assets docs/data` (nested directories)

    Wildcards and brace expansion work with **any command** that accepts paths or arguments.
    For example:
    ```bash
    echo {1..10}   # Prints: 1 2 3 4 5 6 7 8 9 10
    ls *.txt       # List all text files
    ```

=== "Cheat Sheet"

    | Command | Options        | What it does                                                       |
    | :---    | :---           | :---                                                               |
    | `mkdir` | `-p`           | Create directory (+ parent folders)                                |
    | `touch` | -              | Create empty file                                                  |
    | `cp`    | `-r` `-i`      | Copy file or directory (+ recursive for folders)                   |
    | `mv`    | -              | Move or rename (folders too, no -r needed)                         |
    | `rm`    | `-r` `-f` `-i` | Delete permanently (+ recursive, + force, + interactive safe mode) |
    | `rmdir` | `-p`           | Remove empty directories (+ remove parent if empty)                |

    !!! danger "Never run: `rm -rf /` or `rm -rf ~`"

=== "Test your knowledge"

    ## Check Your Understanding

    Test yourself with these real terminal scenarios.

    ### 1. Create a nested project folder

    You're starting a new project for 2024. You want to create this structure all at once:

    ```text
    projects/
    └── 2024/
        └── data/
    ```

    You don't want to type `mkdir projects`, then `mkdir projects/2024`, then `mkdir projects/2024/data`.

    **What command do you type?**

    ??? question "Reveal Answer"

        `mkdir -p projects/2024/data`

        The `-p` flag creates parent directories along the way.

    ---

    ### 2. Backing up a file before editing

    You have `notes.txt`. You want to edit it, but first you want a backup copy called `notes_backup.txt` in the same folder.

    **What command do you type?**

    ??? question "Reveal Answer"

        `cp notes.txt notes_backup.txt`

    ---

    ### 3. Copying a whole project folder

    You have a folder called `projects/` with many files inside. You want to duplicate the entire folder to `projects_backup/`.

    **What command do you type?**

    ??? question "Reveal Answer"

        `cp -r projects/ projects_backup/`

        The `-r` (recursive) flag is needed to copy folders.

    ---

    ### 4. You made a typo in the filename

    You created a file called `reedme.md` but you meant to call it `README.md`.

    **How do you rename it?**

    ??? question "Reveal Answer"

        `mv reedme.md README.md`

    ---

    ### 5. Cleaning up old files

    You have a file called `useless.txt` that you don't need anymore. You want to delete it permanently.

    **What command do you type?**

    ??? question "Reveal Answer"

        `rm useless.txt`

        Remember: `rm` deletes permanently. No trash bin.

    ---

    ### 6. Deleting an old project folder

    You have an old project folder called `old_projects/` with files inside. You want to delete the whole thing.

    **What command do you type?**

    ??? question "Reveal Answer"

        `rm -r old_projects/`

        The `-r` flag deletes folders and everything inside them.

    ---

    ### 7. Moving a file to organize

    You have `file.txt` sitting in your home directory. You want to move it into your `Documents/` folder.

    **What command do you type?**

    ??? question "Reveal Answer"

        `mv file.txt Documents/`

    ---

    ### 8. Creating a README

    You're starting a new project and need an empty `README.md` file.

    **What command do you type?**

    ??? question "Reveal Answer"

        `touch README.md`

    ---

    ### 9. Set up your exercise workspace - Optional

    You want to organize your work for the day. You need a parent folder called `exercises` with 5 subfolders inside it: `exercise_1`, `exercise_2`, `exercise_3`, `exercise_4`, `exercise_5`.

    **What single command creates the entire structure at once?**

    ??? question "Reveal Answer"

        `mkdir -p exercises/exercise_{1..5}`
