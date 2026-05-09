---
title: "Terminal Shortcuts"
description: "Learn essential Linux terminal shortcuts like Tab completion, Ctrl+C, Ctrl+R, and more. Speed up your command line workflow."
---

You can use a mouse and the arrow keys, but what's the fun in that?

> If you don't understand what some of these do, don't worry.  
> Come back to this page after you learn your first commands.

=== "Learn"

    ## Essential Shortcuts

    | Shortcut               | What it does                                  |
    | :---                   | :---                                          |
    | ++tab++                | Auto-complete commands, file names, and paths |
    | ++up++ / ++down++      | Scroll through command history                |
    | ++ctrl+c++             | Cancel/kill the current command               |
    | ++ctrl+l++ or `clear`  | Clear the screen                              |
    | ++ctrl+d++ or `exit`   | Close the terminal / exit the shell           |

    ## Nice-to-Know Shortcuts

    _(Not Essential, But Helpful)_

    | Shortcut                       | What it does                                    |
    | :---                           | :---                                            |
    | ++ctrl+a++                     | Jump to the beginning of the line               |
    | ++ctrl+e++                     | Jump to the end of the line                     |
    | ++ctrl+left++ / ++ctrl+right++ | Jump one word left/right                        |
    | ++ctrl+u++                     | Delete from cursor to the beginning of the line |
    | ++ctrl+k++                     | Delete from cursor to the end of the line       |
    | ++ctrl+w++                     | Delete the word before the cursor               |
    | ++ctrl+r++                     | Search command history                          |

    > "Every shortcut you learn is a tiny speed boost. They add up."

=== "Test your knowledge"

    ## Check Your Understanding

    Test yourself with these real terminal scenarios.

    ### 1. The Forgotten Command

    You typed a command. Then you typed another one. Now you want to run the **first command again** without retyping it.

    **How do you do it?**

    ??? question "Reveal Answer"

        - Press the ++up++ to scroll through your command history until you find it
        - Or ++ctrl+r++ - type part of the command and it searches automatically

    ### 2. The Long Line

    You typed this:

    ```bash
    cd /home/user/Documents/Projects/forgotten-side-project/src/index.html
    ```

    Your cursor is at the end of a long line. You realize you're in the wrong directory and want to **delete the entire line** to start over.

    **Which shortcut do you use?**

    ??? question "Reveal Answer"

        - ++ctrl+u++ - Deletes from cursor to the beginning of the line
        - Or ++ctrl+a++ then ++ctrl+k++ - jump to start, then delete to end

    ### 3. The Terminal is Stuck

    You typed something and hit Enter. Now it's just sitting there. No prompt, no response. It's **stuck** (or just taking forever).

    **How do you get out and try again?**

    ??? question "Reveal Answer"

        - ++ctrl+c++ - Cancels whatever is running and gives you a fresh prompt.
