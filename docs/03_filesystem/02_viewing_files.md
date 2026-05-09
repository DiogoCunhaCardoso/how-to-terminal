---
title: "Viewing Files"
description: "Learn how to view files in the Linux terminal using cat, less, head, and tail. Perfect for reading configs, logs, and text files."
---

You can navigate a filesystem and create files. Now let's read them.

=== "Learn"

    ## File Types

    As written in the intro, file extensions are not interpreted by Linux.
    To check what a file actually is:

    ```bash
    file file_name.jpg   # file_name.jpg: PNG
    ```

    ---

    ## Viewing Files - "Read-Only" Commands

    These commands are safe to use as they won't change your files.

    ### `cat` - Print entire file to screen

    The `cat` command (short for "concatenate") prints the entire content of a file to your terminal.

    ```bash
    cat myfile.txt
    ```

    > Pros: Great for small files. Cons: Floods your screen with long files.

    ### `cat` multiple files

    You can combine files and even create new ones:

    ```bash
    cat file1.txt file2.txt   # prints both files
    ```

    ### Useful options

    | Option | What it does | Example |
    | :--- | :--- | :--- |
    | `-n` | Number all lines | `cat -n script.py` |
    | `-b` | Number non-blank lines only | `cat -b config.conf` |

    ---

    ### `less` - Scroll through files page by page

    `less` is a pager. It shows one page of text at a time. Perfect for long files like logs or configs.

    ```bash
    less myfile.txt
    ```

    | Key                      | Action                                       |
    | ------------------------ | -------------------------------------------- |
    | `Space`                  | Move down one page                           |
    | `b`                      | Move up one page                             |
    | `↓` `↑` / `j` `k`        | Move line by line                            |
    | `/word`                  | Search for "word" (press `n` for next match) |
    | `q`                      | Quit and return to the prompt                |

    > `less` is `more` (it replaced an older command called `more` and added more functionalities). That's the joke.

    ---

    ### `head` and `tail` - View just the beginning or end

    These are useful for quickly checking files.

    ```bash
    head file.txt
    ```
    ```bash
    tail file.txt
    ```

    ### Common Options

    | Option | What it does |
    | :--- | :--- |
    | `-n N` | Show N lines instead of the default 10 |
    | `-f` | Follow a file in real-time (tail only) |

    !!! tip

        `tail -f` shows new lines as they're added. Press ++ctrl+c++ to stop following. Invaluable for watching live logs.

=== "Cheat Sheet"

    | Command | Options | What it does |
    | :--- | :--- | :--- |
    | `file` | - | Identify file type |
    | `cat` | `-n` `-b` | Print entire file (+ line numbers) |
    | `less` | - | Scroll through file page by page |
    | `head` | `-n N` | First N lines (default 10) |
    | `tail` | `-n N` `-f` | Last N lines (default 10), follow live |

    **`less` keys:** `Space` (down page), `b` (up page), `/word` (search), `q` (quit)

=== "Test your knowledge"

    ## Check Your Understanding

    ### 1. Viewing a long file

    You have a log file with thousands of lines. You want to browse it page by page.

    **What command do you use?**

    ??? question "Reveal Answer"
        `less logfile.txt`

    ### 2. Checking a config quickly

    You just want to see the first 5 lines of a config file.

    **What command do you use?**

    ??? question "Reveal Answer"
        `head -n 5 config.conf`

    ### 3. Watching a log in real-time

    A program is writing to `debug.log` and you want to see new lines as they appear.

    **What command do you use?**

    ??? question "Reveal Answer"
        `tail -f debug.log` (press Ctrl+C to stop)

    ### 4. Identifying a file

    You have a file called `unknown` with no extension. You want to know what it actually is.

    **What command do you use?**

    ??? question "Reveal Answer"
        `file unknown`
