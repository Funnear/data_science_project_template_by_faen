# Life hacks for git

## Assign the project root to a variable in a script

[macOS, Linux]

```bash
PROJECT_ROOT="$(git rev-parse --show-toplevel)" ; \
echo "$PROJECT_ROOT"
```

## Add all empty directories to be committed to preserve file structure upfront

Useful for project templates.

[macOS, Linux]

```bash
find . -type d -empty -exec touch {}/.gitkeep \;
```

## List added, deleted, and modified files

Use `--name-status` without filtering to list all changed files and their status relative to
`main`.

[macOS, Linux]

```bash
git diff --name-status main...HEAD
```

The status prefix identifies the change type: `A` for added, `D` for deleted, and `M` for modified.
Git may also report other statuses, such as `R` for renamed or `C` for copied files.

To restrict the output strictly to added and deleted, filter by status.

[macOS, Linux]

```bash
git diff --name-status --diff-filter=AD main...HEAD
```

Prefer Git's `--diff-filter` over piping the output to `grep`, because the filtering is performed
directly by Git and does not depend on external text-processing tools.
