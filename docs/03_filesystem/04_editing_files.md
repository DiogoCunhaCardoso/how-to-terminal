---
title: "Editing Files"
description: "Learn how to edit files from the Linux terminal using Nano and Vim. Includes essential shortcuts for both editors to get you started."
---

Let's learn how to edit files without leaving the terminal.

When you need to change a file, you need a text editor. Linux has many terminal-based editors. Here are the most common ones.

## Built-in editors: Comparison

| Editor   | Learning Curve              | Best For                      | Key Feature                             |
| -------- | --------------------------- | ----------------------------- | --------------------------------------- |
| **Nano** | Low (beginner-friendly)     | Beginners, quick config edits | Shortcuts shown at the bottom           |
| **Vim**  | High (steep learning curve) | Power users, developers       | Modal editing (super fast once learned) |

**Recommendation:** Start with **Nano**. It's installed everywhere and works like a simple notepad. You can learn Vim later if you want to.

---

### Nano Editor

```bash
nano myfile.txt
```

- If myfile.txt exists, Nano opens it.
- If it doesn't exist, Nano creates it when you save.

### Essential Nano Shortcuts

When time comes you will get into the rabbit whole of editors. For now here are some shortcuts.

| Shortcut            | What it does                         |
| ------------------- | ------------------------------------ |
| ++ctrl+x++          | Exit (asks to save if changes exist) |
| ++ctrl+o++          | Save ("Write Out" the file)          |
| ++ctrl+w++          | Search for text                      |
| ++ctrl+k++          | Cut the current line                 |
| ++ctrl+u++          | Paste the cut line                   |
| ++ctrl+underscore++ | Go to a specific line number         |
| ++ctrl+c++          | Show cursor position (line/column)   |
| ++ctrl+g++          | Open help menu                       |

!!! tip "Lost in Nano?"

    Look at the bottom two lines of your terminal. Nano shows shortcuts there.

### Vim Editor

!!! quote "Optional - Want more power? Try Vim"

    Vim is another terminal editor. If it's your first time you will feel lost using it.
    It has a steep learning curve but is very powerful.

Vim is a modal editor, meaning it has different "modes" for different tasks. This is the biggest difference from Nano and the main reason for its steep learning curve.

```bash
vi myfile.txt
```

- If myfile.txt exists, Vim opens it.
- If it doesn't exist, Vim creates it when you save.

A short follow along:

| Step | Action                               |
| :--- | :----------------------------------- |
| 1    | Press `i` (enter Insert mode)        |
| 2    | Type `Hello World from Vim`          |
| 3    | Press `Esc` (back to Normal mode)    |
| 4    | Type `:wq` + `Enter` (save and quit) |

> Vim deserves a full course since it has many many features. There's a meme that people use Vim to this day because they were never able to quit Vim.
