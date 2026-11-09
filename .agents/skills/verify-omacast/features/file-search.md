# File search

File search shows files and folders from the home folder in a Files section of the main search, and in the Search Files view with a preview pane. The user opens a file or folder, shows it in the file manager, or copies its path. Files that the user opens rank higher later.

## Sub-features

- `files-section` shows matching files and folders under the heading Files, after Results.
- `files-rank` puts exact names first, then name prefixes, then word starts. Newer items win ties.
- `files-select` selects the first file when nothing else matched.
- `files-open` opens the selected file in its default app, or a folder in Files.
- `files-show` opens Files with the item selected.
- `files-copy-path` copies the full path.
- `files-empty` shows no Files section when nothing matches or the query is one character.
- `files-learn` ranks a file higher after the user opens it. The rank survives a reload.
- `sf-open` opens the Search Files view from the root command, or with the query from Search All Files in the action panel.
- `sf-recent` lists recently changed files before the user types.
- `sf-preview` shows an image, the head of a text file, or a type glyph, and the Name, Where, Type, Size, and Modified rows.

## How to get to it (user POV)

- Press Ctrl+Space outside a terminal and type part of a file name.
- In the action panel (Ctrl+K) on a file row, choose Open File, Show in Files, Copy Path, or Search All Files.
- Type `search files` in the launcher and press Enter.

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
- **Learn.** Run `vo search "zebrafish"` and note the order. Run `vo open "zebrafish photo"` and `vo key Return`. An image viewer window opens. Run `vo search "zebrafish"`. `zebrafish-photo.png` is now first. Run `vo reload` and search again. It is still first.
- **Search Files view.** Run `vo open "search files"`. `omarchy-shell omacast selected` prints `builtin:search-files`. Run `vo key Return` and `vo shot sf-recent`. The crop shows the heading `Recently Changed`, a narrow list, and a detail pane.
- **Preview.** Run `vo type "zebrafish"`. Run `vo shot sf-notes`, `vo key Down`, `vo shot sf-photo`, `vo key Down`, and `vo shot sf-budget`. The crops show the Markdown text, the gradient image with the word zebrafish, and the CSV text. The detail rows show `~/omacast-verify`, `Image`, `Spreadsheet`, and `Mar 2025`.
- **Carry the query.** Run `vo open "zebrafish"`, `vo key ctrl+k`, `vo type "search all"`, and `vo key Return`. The Search Files view opens with the query `zebrafish`.
- **Proof.** Keep `files-section-crop.png`, the `vo new-windows` output, and the `wl-paste` output in the run folder.

## Gotchas

- The fixture is new, so the 30-second refresh can hide it. Run `vo open` once, close the launcher, wait 30 seconds, and open again. Or run `omacast reload`, which starts with an empty list.
- Hidden folders and `node_modules`, `.venv`, `venv`, `__pycache__`, `site-packages`, `target`, `.cache`, and `.git` are not listed. This is intended.
- A query that matches only a folder name does not list the files inside it.
- Open uses `gio open`. A `.txt` file opens nvim inside a foot terminal. `xdg-open` would start nvim with no window.
- `vo reload` before a drive after a code change. A plain `omacast reload` leaves the old instance answering for a moment.
- Opening a fixture file adds a `file:` entry to `~/.local/share/omacast/db/frecency.json`. The entry stays after cleanup. It is harmless because the file is gone.
- The fixture files open in real apps. `vo clean` closes only the windows in the `vo new-windows` list.
