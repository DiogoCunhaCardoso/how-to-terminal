---
title: "Intro"
description: "Learn the basic structure of Linux commands. What options and arguments are, and how to combine them."
---

Let's finally start typing! All commands in this guide are for **Bash** (the default on most Linux systems).

=== "Learn"

    Open a terminal and type your first command.

    ```bash
    echo Hello World
    ```

    > You should see "Hello World" being written back by the terminal

    ## Command Anatomy

    Every command you'll type follows the same pattern:

    ```
    COMMAND [...OPTIONS] [...ARGUMENTS]
       ↓          ↓            ↓
      What       How         Where

    ```

    > `[ ]` means optional. You don't always need options or arguments. `...` means multiple.

    Example:

    | Part          | Meaning                   | Example: `ls -l Documents/` |
    | :------------ | :------------------------ | :--------------------------- |
    | **COMMAND**   | What you want to do       | `ls` (list files)            |
    | **OPTIONS**   | How to modify the command | `-l` (long/detailed format)  |
    | **ARGUMENTS** | Where it applies          | `Documents/` (the folder)    |

    ### Multiple Options

    You can use more than one option at a time.

    ```bash
    ls -l -a -h
    ```

    !!! tip "Combine options:"

        Order does not matter: `-lah`, `-lha`, `-alh` - all work the same.

=== "Test your knowledge"

    ## Check Your Understanding

    Even without knowing these commands, you can figure out each part just by looking at the pattern.

    What is the command? What is the option? What is the argument?

    ### 1. Command

    ```bash
    pwd
    ```

    ??? question "Reveal Answer"

        - Command: pwd
        - Options: none
        - Arguments: none
    ### 2. Command

    ```bash
    ls -lh stuff/
    ```

    ??? question "Reveal Answer"

        - Command: ls
        - Options: -lh
        - Arguments: stuff/

    ### 3. Command

    ```bash
    ls -a
    ```

    ??? question "Reveal Answer"

        - Command: ls
        - Options: -a
        - Arguments: none
