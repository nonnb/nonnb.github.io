# Git-Notes Integration *(experimental in 25.1)*

This article explains how to configure and enable **SmartGit’s Git-Notes features** through ordinary Git configuration files.

---

## Contents
- [Minimal setup](#minimal-setup)
- [`smartgit-notes` section](#smartgit-notes-section)
  - [Keys](#keys)
  - [Colour format](#colour-format)
- [Default behaviour when no section is present](#default-behaviour)
- [Example configurations](#example-configurations)
- [Configuration best practices](#configuration-best-practices)

---

## Enabling Notes features in SmartGit on a repository

In order for SmartGit notes to be enabled, SmartGit needs to find either:

- The presence of `refs/notes/commits`, which is the default Git notes category ref (e.g. as created by a `git notes add -m '..'` command).
- One or more `[smartgit-notes]` subsections defined in the Git configuration.

If `refs/notes/commits` is found, SmartGit automatically creates an implicit notes category called **“Notes”** that tracks `refs/notes/commits`.

## Minimal [smartgit-notes] configuration

Add one or more subsections under `smartgit-notes` to describe the *categories* of notes you want SmartGit to show:

```ini
[smartgit-notes "<category-id>"]
    # all keys are optional – see below
    ref              = <notes-ref>
    graphMessageRegex= <regex>
    color            = <RRGGBB>
```

SmartGit reads these directives from the repository’s local `.git/config`, the user-wide `~/.gitconfig`, or the system config – and reloads changes automatically for the local repo.
A restart is only needed when you edit user or system-wide configs.

#### Tip
> 
> The name and colour of the default `commits` ref category can be overridden in the SmartGit UI by adding a `smartgit-notes` section for the default `ref = commits` category.
> See [below](#1-–-override-classic-commits-notes) for details
>
---

## `smartgit-notes` section

### Keys

| Key | Required | Purpose |
|-----|----------|---------|
| **`ref`** | no (defaults to the subsection’s name) | Path **relative to `refs/notes/`** that stores the notes for this category. You may also specify the full ref (`refs/notes/xyz`); the leading prefix will be stripped automatically. |
| **`graphMessageRegex`** | no | Java regular expression; if present, SmartGit shows the extracted text instead of the generic notes icon. |
| **`color`** | no | Hex RGB triplet (e.g. `FFCC00`), rendered in the log graph for this category. The value is parsed as a 24-bit integer, so **omit the leading `#`**. |

---

## Example configurations

### 1 – Override Classic *commits* notes

```ini
[smartgit-notes "Personal Notes"]
    # same as the default, but defined explicitly
    ref              = commits
    color = 5DADEC   # light-blue in the graph
```

### 2 – Separate *code-reviews* category with filtering

```ini
[smartgit-notes "reviews"]
    ref               = code-reviews        # stored at refs/notes/code-reviews
    graphMessageRegex = ^Review[ed]?:        # show only when the commit
                                             # message starts with “Review:”
    color             = FF8800              # orange
```

### 3 – Multiple categories side-by-side

```ini
[smartgit-notes "qa"]
    ref   = qa          # refs/notes/qa
    color = 66CC66      # green

[smartgit-notes "design"]
    ref   = ux-design   # refs/notes/ux-design
    color = CC66CC      # purple
```

---

## Configuration best practices

1. **Global vs. local** – You can keep common categories (e.g. *commits*) in `~/.gitconfig` but declare project-specific ones in each repo’s `.git/config`.
2. **Ref naming** – Use short, descriptive subsection names; if you omit `ref`, SmartGit will fall back to that name, keeping your config concise.
3. **Colour palette** – Pick sufficiently different colours so each category is recognisable in the log graph.
4. **Regular expressions** – Keep `graphMessageRegex` simple and anchored (`^…`) to avoid accidental matches that hide or show unexpected commits.

With these settings in place you can toggle Git-Notes columns in SmartGit’s **Log Window** and enjoy a colour-coded, filtered view of your notes alongside normal commit data.

---

LLP:
- log.graph.draw.iconNotes -> for users
- gitnotes.showInvisibleNotes -> probably just for testing
- gitnotes.allowRemovingAllNotes -> definitely just for testing
