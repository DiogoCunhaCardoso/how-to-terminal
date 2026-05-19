---
title: "Get Started"
description: "Learn the difference between Linux, Shell, Terminal, and Distribution. Start your command line journey with this beginner-friendly guide."
---

Let's get some basics out of the way first. Then you can start typing.

## Terminology

=== "Learn"

    ### What is Linux?

    **Linux is a kernel.**

    A kernel is the core component of an OS.
    It decides which program gets CPU, memory, and disk attention.

    > Without a kernel, your hardware does nothing.

    ```
    ┌──────────────────┐              ┌──────────────────────────────────────────────┐
    │ OPERATING SYSTEM │              │                  HARDWARE                    │
    │ ┌──────────────┐ │              │  ┌─────┐  ┌──────┐  ┌────────┐  ┌─────────┐  │
    │ │    KERNEL    │─│ ─ Manages ─> │  │ CPU │  │ DISK │  │ MEMORY │  │ DEVICES │  │
    │ └──────────────┘ │              │  └─────┘  └──────┘  └────────┘  └─────────┘  │
    └──────────────────┘              └──────────────────────────────────────────────┘
    ```

    But a kernel alone is useless. That's where distributions come in.

    ---

    ### What is a Distro?

    Distribution (or _distro_) = kernel + everything else you need to actually use the computer.

    The "everything else" includes:

    - Graphical interface _(what you click)_
    - File manager
    - Drivers _(eg. Wi-Fi, Bluetooth)_
    - Pre‑installed apps

    All this together = the Operating System.

    !!! info "Popular Beginner Distros: Ubuntu (The most famous) - Mint (Feels like Windows)"

    ---

    ### What is a Shell?

    A shell is a program that interprets commands and knows how you speak to the kernel.

    You type something.
    The shell translates it.
    The kernel executes it.

    | Shell          | Found on     | Notes                                   |
    | :------------- | :----------- | :-------------------------------------- |
    | **Bash**       | Linux, macOS | Available on macOS (not the default)    |
    | **Zsh**        | macOS        | Default since Catalina (2019)           |
    | **PowerShell** | Windows      | ---                                     |

    !!! tip "Want to stay on Windows?"
        Install [WSL](https://learn.microsoft.com/en-us/windows/wsl/install){: target="_blank" } to use Bash.

    ---

    ### What is a Terminal?

    A terminal is the UI window that runs the shell.

    ---

    ### Flow: Using a Command

    This is what happens when you type a command called `ls` into the terminal.

    ```
    ┌──────┐     ┌──────────┐     ┌────────────┐     ┌───────────┐     ┌──────────┐
    │ YOU  │  →  │ TERMINAL │  →  │   SHELL    │  →  │   KERNEL  │  →  │ HARDWARE │
    ├──────┤     ├──────────┤     ├────────────┤     ├───────────┤     ├──────────┤
    │ "ls" │     │ (Window) │     │(Language + │     │ (Manager) │     │  (Body)  │
    └──────┘     └──────────┘     │interpreter)│     └───────────┘     └──────────┘
                                  └────────────┘
      "ls"        keystrokes        finds "ls"        manages "ls"    disk reads bits
     +Enter                       asks permission
    ```

    ### What is a Partition?

    !!! quote "Optional information"
        Most distros handle partitions automatically. It's good to know, for example, if you ever install Windows + Linux on the same computer (dual-boot).

    A partition is a slice of your hard drive that acts like a separate disk.


    Common Linux partitions:

    | Partition | Purpose | Size |
    | :--- | :--- | :--- |
    | `/` (root) | System lives here | 20-30 GB |
    | `/home` | Your personal files | rest of disk |
    | `swap` | Emergency RAM | 2-4 GB |
    | `/boot` | Linux startup files | ~500 MB |

=== "Cheat Sheet"

    | Concept | One sentence                                         |
    | :---             | :---                                        |
    | **Linux**        | A kernel - a program that manages hardware and resources |
    | **Distribution** | Kernel + everything else (an OS)            |
    | **Shell**        | A program that interprets commands          |
    | **Terminal**     | The window where you speak a shell language |
    | **Partition**    | A slice of your hard drive                  |

=== "Test your knowledge"

    ## Check Your Understanding

    Test yourself with these theoretical questions.

    ### 1. Is Ubuntu an operating system or a kernel?

    ??? question "Reveal Answer"
        Ubuntu is an **operating system** (a Linux distribution)

    ### 2. What's the difference between a shell and a terminal?

    ??? question "Reveal Answer"
        **Terminal** = window. **Shell** = program that runs inside it (Bash, Zsh) and interprets what you type

    ### 3. Which partition holds your personal files?

    ??? question "Reveal Answer"
        `/home`

    ### 4. What does the kernel actually *do*?

    ??? question "Reveal Answer"
        Manages CPU, memory, disk, and devices - decides which program gets what and when
