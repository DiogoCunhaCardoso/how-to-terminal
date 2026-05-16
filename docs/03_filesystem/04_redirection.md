---
title: "Redirection"
description: "Learn how to redirect Linux command output using >, >>, 2>, and |. Save output to files, append to logs, capture errors, and pipe between commands."
---

Every command has three standard connections to the outside world:

=== "Learn"

    | Connection | Number Associated | What it does                           |
    | :--------- | :-----            | :------------------------------------- |
    | **stdin**  | 0                 | Standard input (usually your keyboard) |
    | **stdout** | 1                 | Standard output (usually your screen)  |
    | **stderr** | 2                 | Standard error (error messages)        |

    You've been using stdin, stdout, and stderr already. You just didn't know the names.

    - When you type `echo "Hello"` - you see "Hello" on screen (that's **stdout**)
    - When you type `ls fakefile.txt` - you see an error on screen (that's **stderr**)
    - When you type a command - your keyboard sends input (that's **stdin**)

    Redirection lets you change where these connections go. For example, to files instead of your screen.

    ---

    ## `>` - Save output to a file (stdout)

    Instead of printing to your screen, send the output to a file.

    ```bash
    ls > files.txt
    ```

    What happens:

    - ls runs normally
    - Output goes to files.txt instead of your screen
    - If files.txt exists, it gets overwritten

    ```bash
    echo "Hello" > hello.txt   # creates hello.txt with "Hello"
    cat hello.txt
    # Hello

    cat file1.txt file2.txt > merged.txt # merge two files into one new file
    ```

    > `>` default is `1>` - meaning stdout, so no need to write the number 1.

    ---

    ## `>>` - Append output to a file (add, don't overwrite)

    Same as `>`, but adds to the end instead of overwriting.

    ```bash
    echo "First line" > file.txt
    echo "Second line" >> file.txt
    cat file.txt
    # First line
    # Second line
    ```

    > Use >> when you want to keep what's already there.

    ---

    ## `2>` - Save error messages (stderr)

    By default, error messages go to your screen too. `2>` captures only errors.

    ```bash
    ls fakefile.txt 2> errors.txt
    cat errors.txt
    # ls: cannot access 'fakefile.txt': No such file or directory
    ```

    ### Combining stdout and stderr

    | Syntax | What it does |
    | :--- | :--- |
    | `command > output.txt 2>&1` | Send both stdout and stderr to same file |
    | `command &> output.txt` | Same as above (shorter) |

    ```bash
    ls legit.txt fake.txt &> all.txt   # both output and error go to all.txt
    ```

    ---

    ## `|` - Pipe: send output from one command to another

    The pipe `|` takes the stdout of the left command and passes it as stdin to the right command.

    ```bash
    ls -la | head -n 5
    # Shows only the first 5 lines of ls output
    ```

    > You can chain pipes - `[command1] | [command2] | [command3]`

=== "Cheat Sheet"

    | Symbol | What it does                        | Example                          |
    | :---   | :---                                | :---                             |
    | `>`    | Save stdout to file (overwrite)     | `ls > files.txt`                 |
    | `>>`   | Append stdout to file               | `echo "Second line" >> file.txt` |
    | `2>`   | Save stderr to file                 | `ls fakefile.txt 2> errors.txt`  |
    | `2>&1` | Send stderr to same place as stdout | `ls > all.txt 2>&1`              |
    | `|`    | Pipe stdout to another command      | `ls -la | head -n 5`             |

=== "Test your knowledge"

    ## Check Your Understanding

    Test yourself with these real terminal scenarios.

    ### 1. Save a directory listing

    You want to save the output of `ls -la` to a file called `directory.txt`.

    **What command do you type?**

    ??? question "Reveal Answer"

        ```bash
        ls -la > directory.txt
        ```

    ### 2. Add to a log file

    You want to add the current date to events.log without erasing what's already there.

    **What command do you type?**

    ??? question "Reveal Answer"

        ```bash
        date >> events.log
        ```

    ### 3. Capture errors only

    You run `ls fakefile.txt realfile.txt` and only want to save the error message to `errors.txt`.

    **What command do you type?**

    ??? question "Reveal Answer"
        ```bash
        ls fakefile.txt realfile.txt 2> errors.txt
        ```
