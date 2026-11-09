# File search

File search shows files and folders from the home folder in a Files section of the main search. The user opens a file or folder, shows it in the file manager, or copies its path.

## Sub-features

- `files-section` shows matching files and folders under the heading Files, after Results.
- `files-rank` puts exact names first, then name prefixes, then word starts. Newer items win ties.
- `files-select` selects the first file when nothing else matched.
- `files-open` opens the selected file in its default app, or a folder in Files.
- `files-show` opens Files with the item selected.
- `files-copy-path` copies the full path.
- `files-empty` shows no Files section when nothing matches or the query is one character.

## How to get to it (user POV)

- Press Ctrl+Space outside a terminal and type part of a file name.
- In the action panel (Ctrl+K) on a file row, choose Open File, Show in Files, or Copy Path.

## Driving it with vo

Preconditions:

- `vo doctor` shows `file index method present` as ok.
- `vo fixture` created `~/omacast-verify/zebrafish-notes.md` and `~/omacast-verify/Reports/zebrafish-budget.csv`.
- `vo open` ran once after the fixture, so the file list includes it. The list refreshes when the launcher opens and is older than 30 seconds.

- **Section.** Run `vo open "zebrafish"`. Then run `vo search "zebrafish"`. The Files section lists `zebrafish-notes.md` first and `zebrafish-budget.csv` second. The notes row shows `~ › omacast-verify` and a relative time. The budget row shows `~ › omacast-verify › Reports` and `Mar 2025`.
- **Selection.** Run `vo shot files-section`. The crop shows `zebrafish-notes.md` selected and the footer reads `Open File`.
- **Open.** Run `vo windows-before`, then `vo key Return`. Then run `vo new-windows`. One new window appears. Its title contains `zebrafish-notes`. Markdown opens in the user's Markdown app (WordCraft on this machine).
- **Show in Files.** Run `vo open "zebrafish budget"`, then `vo key ctrl+Return`. `vo new-windows` lists a new `org.gnome.Nautilus` window for the folder `Reports`.
- **Copy path.** Run `vo open "zebrafish notes"`, then `vo key ctrl+shift+c`. `wl-paste` prints `/home/<user>/omacast-verify/zebrafish-notes.md`.
- **Empty.** Run `vo search "zebrafishqqq"`. No Files section. Run `vo search "z"`. No Files section.
- **Proof.** Keep `files-section-crop.png`, the `vo new-windows` output, and the `wl-paste` output in the run folder.

## Gotchas

- The fixture is new, so the 30-second refresh can hide it. Run `vo open` once, close the launcher, wait 30 seconds, and open again. Or run `omacast reload`, which starts with an empty list.
- Hidden folders and `node_modules`, `.venv`, `venv`, `__pycache__`, `site-packages`, `target`, `.cache`, and `.git` are not listed. This is intended.
- A query that matches only a folder name does not list the files inside it.
- Open uses `gio open`. A `.txt` file opens nvim inside a foot terminal. `xdg-open` would start nvim with no window.
- The fixture files open in real apps. `vo clean` closes only the windows in the `vo new-windows` list.
