---
name: verify-omacast
description: Drive the live omacast launcher (Omarchy shell plugin, Ctrl+Space) the way a user does and save proof. Use before you say an omacast change works, for any check of search results, file search, the action panel, opening files or apps, and keyboard behavior. Read features/README.md first.
---

# Verify omacast

omacast is a plugin inside `omarchy-shell`, the one Quickshell process that also draws the bar. There is only one instance. It is the user's real desktop. You cannot start a second copy side by side.

The helper `bin/vo` does every step. Run it by its path:

```bash
VO=~/Projects/oma-cast/.agents/skills/verify-omacast/bin/vo
$VO --help
```

## Safety rules

1. Each run shows the launcher on the user's screen. Keep runs short.
2. Send keys only with `vo key` or `vo type`. They refuse when the launcher is closed. A key sent to a closed launcher goes to the window underneath, often the user's terminal.
3. Clear the query before you type. The launcher keeps the old query between opens. `vo open <query>` sets the query for you.
4. Never press Enter on a web-search row. It opens real browser tabs.
5. Close only windows that this run opened. `vo clean` does this from the `vo windows-before` list.
6. If the user is typing or moving windows during a run, stop. Their input mixes with yours and the proof is invalid.

## Launch

The shell is already running. Load the current code into it:

1. The code is in `~/Projects/oma-cast`. The plugin folder `~/.config/omarchy/plugins/typecraft.omacast` is a symlink to it.
2. After you edit QML or JS, run `vo reload`. Quickshell caches every QML file it read, so a plain save does not load new code.
3. `vo reload` waits until the new plugin instance is ready. The old instance answers for a moment after `omacast reload` and drops what it gets, so do not use `omacast reload` alone before a drive.
4. Read the shell log for QML errors: `qs log -n -p "$OMARCHY_PATH/shell" -t 50 | grep -i omacast`. "Type X unavailable" means a QML error. The cause is on the next line.

If `omacast reload` refuses ("for development checkouts"), the plugin folder is a real folder, not a symlink. Then run `omarchy restart shell`. This restart redraws the bar, so tell the user.

`omacast reload` renames the plugin link to `typecraft.omacast.dev-<number>`. `omarchy plugin update` needs the plain name. When the work is done, restore it with `~/Projects/oma-cast/bin/omacast install`.

Teardown: there is nothing to stop. Run `vo clean`.

## Doctor

Run `vo doctor` first, and again when anything looks wrong. It checks the shell, the IPC, the backend, and that the loaded build has file search. It prints the plugin path, the git branch, and the file index state. Do not drive the launcher when a line says FAIL.

## Drive

1. `vo start <name>` creates the evidence folder and prints its path.
2. `vo open "<query>"` shows the launcher with that query. It waits until the launcher is open and the file list loaded.
3. `vo search "<query>"` prints the sections and rows that the launcher shows. It calls the same backend method as the UI. Use it to read row ids and order.
4. `vo key Down`, `vo key Return`, `vo key ctrl+k`, `vo key Escape` press keys in the launcher. `vo type "text"` types text.
5. `vo shot <name>` saves a screenshot of the launcher's monitor and a centre crop.
6. `vo windows-before` before an action that opens a window. `vo new-windows` after it prints the new windows.
7. `vo hide` closes the launcher.

The feature recipes are in `features/`. Use the matching file for the exact steps.

## Evidence

Evidence goes to `~/.local/state/omacast-verify/<time>-<name>/`. `vo clean` never deletes it.

A proof has:

1. A screenshot of the launcher before the action. It shows the query and the selected row.
2. The result of the action: a screenshot, the `vo new-windows` output, or the clipboard (`wl-paste`).
3. For a side effect, a second view of it. Example: the window title of the opened file, not only the launcher closing.

Use the real user path: keys in the launcher. Do not call `rootSearch.performAction` directly to prove an action. Use `vo search` only to read results.

## Cleanup

Run `vo clean`. It hides the launcher, closes the windows that this run opened, and deletes `~/omacast-verify/`. It prints the evidence folder. Check that the evidence files still exist after cleanup.

## Unit tests

Unit tests are separate from this skill. Run `node --test tests/*.test.js` in `~/Projects/oma-cast`. Run `omarchy plugin validate .` before a commit.
