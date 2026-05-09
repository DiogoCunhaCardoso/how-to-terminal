---
title: "Navigation Commands"
description: "Learn how to navigate the Linux filesystem using pwd, ls, and cd. Understand paths and shortcuts"
---

Now that you understand the filesystem tree, let's learn how to move around.

=== "Learn"

    ## `pwd` - Where am I?

    `pwd` stands for **P**rint **W**orking **D**irectory. It tells you exactly where you are.

    ```bash
    pwd   # /home/your-username
    ```

    ## `ls` - What's here?

    `ls` stands for List. It shows you what's inside the current directory.

    ```bash
    ls   # Documents  Downloads  Desktop  Pictures  Music  Videos
    ```

    ### Common Options

    | Option | Meaning        | Why you need it                                     |
    | :----- | :------------- | :-------------------------------------------        |
    | `-l`   | Long format    | See file sizes, dates, permissions                  |
    | `-a`   | All files      | See hidden files - files starting with `.`          |
    | `-h`   | Human-readable | Makes `-l` output readable - `4K` not `4096`        |

    ### Nice to know

    | Option | Meaning      | Why you need it                  |
    | :----- | :----------- | :------------------------------- |
    | `-R`   | Recursive    | Explore entire folder structures |
    | `-t`   | Sort by time | Find recently changed files      |
    | `-S`   | Sort by size | Find what's taking up space      |

    ## `cd` - Move around

    `cd` stands for **C**hange **D**irectory. It moves you somewhere else.

    ```bash
    cd Documents/  # Puts you inside Documents directory
    ```

    !!! tip "Tab Autocomplete & Conflicts"
        If you type `cd Do` + ++tab++ and nothing happens, there is a conflict (e.g., **Documents** vs **Downloads**). Press ++tab++ twice to see all available options.

    ### Path Types

    **Absolute paths** work no matter where you are. **Relative paths** depend on your current location.

    | Type         | Starts with | Example                                                      |
    | :---         | :---        | :---                                                         |
    | **Absolute** | `/`         | `/home/your-username/Documents`                              |
    | **Relative** | NOT `/`     | `Documents/` - only works if you're in `/home/your-username` |

    ### Special Path Shortcuts

    These symbols save you typing:

    | Shortcut | What it means                   |
    | -------- | ------------------------------- |
    | `.`      | Current directory               |
    | `..`     | Parent directory (one level up) |
    | `~`      | Your home directory             |
    | `/`      | Root directory                  |

    > `cd ..` is the one you'll use constantly.

    If you type `cd` by itself (no path), it takes you straight home:

    ```bash
    cd         # same as cd ~
    pwd        # /home/your-username
    ```

=== "Cheat Sheet"

    | Command | Common Options | What it does |
    | :--- | :--- | :--- |
    | `pwd` | - | Where am I? |
    | `ls` | `-l` `-a` `-h` `-R` `-t` `-S` | List files (+ options for details, hidden, human, recursive, time, size) |
    | `cd` | `folder/` `..` `~` `/` | Move around (enter, up, home, root) |

    **Shortcuts:** `.` = here, `..` = up, `~` = home, `/` = root

=== "Test your knowledge"

    ## Check Your Understanding

    Test yourself with these real terminal scenarios.

    ### 1. Where am I?

    You just opened your terminal. You have no idea where you are.

    **What command do you type?**

    ??? question "Reveal Answer"
        `pwd` - Prints your current location.

    ---

    ### 2. What's here?

    You want to see what files and folders are in your current directory.

    **What command do you type?**

    ??? question "Reveal Answer"
        `ls` - Lists everything in the current directory.

    ---

    ### 3. Enter a folder

    You see `Documents` in the list. You want to go inside it.

    **What command do you type?**

    ??? question "Reveal Answer"
        `cd Documents/` - Moves you into the Documents folder.

    ---

    ### 4. Go up one level

    You're in `Documents`. You want to go back to the previous folder.

    **What command do you type?**

    ??? question "Reveal Answer"
        `cd ..` - Moves up one level to the parent directory.

    ---

    ### 5. Go home

    You're deep inside some folder. You want to go straight back to your home directory.

    **What command do you type?**

    ??? question "Reveal Answer"
        `cd` or `cd ~` - Both take you home.

    ---

    ### 6. Go to root

    You want to go to the very top of the filesystem.

    **What command do you type?**

    ??? question "Reveal Answer"
        `cd /` - Takes you to root.

    ---

    ### 7. See hidden files

    You run `ls` but don't see your `.bashrc` file. You know it exists somewhere.

    **What command do you type?**

    ??? question "Reveal Answer"
        `ls -a` - Shows all files, including hidden ones (starting with `.`).

    ---

    ### 8. See file details

    You want to see file sizes, dates, and permissions - not just names.

    **What command do you type?**

    ??? question "Reveal Answer"
        `ls -l` - Long format shows details.

    ---

    ### 9. Human-readable sizes

    You run `ls -l` but see `4096` instead of `4K`. You want it readable.

    **What command do you type?**

    ??? question "Reveal Answer"
        `ls -lh` - Adds `-h` for human-readable sizes.
