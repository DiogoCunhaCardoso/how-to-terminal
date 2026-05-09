# Contributing to How to Terminal

Every contribution helps someone learn the terminal. Thank you.

---

## Quick Rules

| Rule                | Description            |
| :------------------ | :--------------------- |
| **English first**   | Write in English       |
| **Small PRs**       | Keep changes focused   |
| **Match the style** | Look at existing pages |

---

## What to contribute

- Fix typos, grammar, or confusing explanations
- Add missing examples
- Propose a better organization
- Write new lessons (follow the pattern below)
- etc.

---

## Page Pattern

````markdown
---
title: "Page Title"
description: "SEO description"
---

Short intro (human, friendly)

=== "Learn"

    ## Command - What it does

    ```bash
    command example
    ```

    ### Options (if any)

    | Option | What it does   |
    | :---   | :---           |
    | `-x`   | Does something |

=== "Cheat Sheet"

    | Command | Options | What it does   |
    | :---    | :---    | :---           |
    | `cmd`   | `-x`    | Does something |

=== "Test your knowledge"

    ## Check Your Understanding

    1. Question One

    ??? question "Reveal Answer"
    Answer here
````

> Use `!!! tip`, `!!! info`, or `!!! danger` where needed.

> If it is a new topic make sure the intro.md descriptions gets an update.

> Intro pages (`intro.md`) are allowed to stay simple and should not be forced into the `=== "Learn"` / `=== "Cheat Sheet"` / `=== "Test your knowledge"` tabbed pattern.

---

## Adding a page

1. Create a `.md` file in `docs/`
2. Add its path to `nav` in `zensical.toml`

---

## Development Process

1. **Fork** the repository
2. **Create a branch**: `git checkout -b fix/typo-intro`
3. **Make your changes** (follow the style)
4. **Test locally**: `zensical serve`
5. **Submit a PR** with a clear description

---

## Questions?

Open an issue. Be respectful.

---

> _"Every contribution helps someone learn the terminal."_
