# omacast verification map

This folder is the source for verifying what an omacast user sees and does. Read this index first. Then use the matching feature file as the recipe.

## Baseline preconditions

- `vo doctor` shows no FAIL line.
- The launcher is closed. `omarchy-shell omacast isOpen` prints `false`.
- A run is started with `vo start <name>`.
- For file search, the fixture exists. Run `vo fixture`.

## Driving conventions

- Open the launcher with `vo open "<query>"`. Do not type into a stale query.
- Send keys only with `vo key` and `vo type`.
- Read results with `vo search "<query>"`. Prove actions with keys, not with direct backend calls.
- Run `vo windows-before` before any action that can open a window.
- End every run with `vo clean`.

## Proof and skip reporting

- Capture the state before the action and the result after it.
- Prove side effects with a second view: the new window, the clipboard, or a file.
- Record the feature ID with each artifact name, for example `file-search-open.png`.
- Report a path you could not reach with the command and the unmet precondition.
- Do not report a skipped entry point as verified through another path.

## Feature entry contract

Each feature file has an H1 title and one paragraph. Then it has four H2 sections in this order: `Sub-features`, `How to get to it (user POV)`, `Driving it with vo`, and `Gotchas`.

## Features

- [File search](./file-search.md) covers the Files section, open, show in Files, copy path, and empty results.
- [Root search](./root-search.md) covers apps, Omarchy commands, and web fallbacks.
- [Calculator](./calculator.md) covers the inline answer and copy.
- [Action panel](./action-panel.md) covers Ctrl+K and the About panel.
