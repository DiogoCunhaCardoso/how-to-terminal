---
title: "Intro"
description: "Learn Linux file naming conventions: case sensitivity, allowed characters, and why extensions are just hints. Get ready to create, move, copy, and delete files."
---

Navigation taught you how to **move around**. Now let's learn how to **change things**.

You'll learn how to:

- **Create** files and folders
- **Move, copy, and delete** them
- **View and edit** what's inside

---

## Linux naming conventions

**Case sensitive** : `File.txt` ≠ `file.txt`

**Use only:** letters, numbers, `-`, `_`, `.`

**Avoid:** spaces, `*`, `?`, `$`, `!`, `@`, `#`, `(`, `)`, `/`

**Extensions are just hints**: Linux ignores them. `photo.jpg` might be a PNG. Still use extensions to help yourself (and others).

```bash
good_names.txt
my-document.md
notes_2024.txt

bad name.txt   # needs quotes or escapes
what?.md       # ? is special to the shell

```

!!! warning "Spaces need quotes"

    To use a file named with spaces like `my notes.txt`, write it as:

    ```bash
    [command] "my notes.txt"
    # or [command] my\ notes.txt
    ```

> On macOS or Windows, readme.md and README.md are the same file. On Linux, they are different. This can cause merge conflicts if you share files between systems (like Git repos).
