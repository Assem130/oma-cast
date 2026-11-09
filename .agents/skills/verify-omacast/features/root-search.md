# Root search

Root search finds apps and Omarchy menu actions from one query. When nothing fits, it offers web searches.

## Sub-features

- `root-empty` shows Favorites, Suggestions, Commands, and Applications with no query.
- `root-results` ranks apps and Omarchy actions in a Results section for a query.
- `root-breadcrumb` shows the Omarchy menu path of an action, for example `Trigger › Capture`.
- `root-fallback` shows `Use "<query>" with…` with Search Google and Search DuckDuckGo.
- `root-open-app` focuses an open app window, or starts the app.

## How to get to it (user POV)

- Press Ctrl+Space outside a terminal. Type an app or action name.

## Driving it with vo

Preconditions:

- `vo doctor` shows no FAIL line.

- **Empty root.** Run `vo open ""` and `vo shot root-empty`. The crop shows section headings and app rows.
- **Results.** Run `vo search "screenshot"`. The Results section contains `Screenshot` with subtitle `Trigger › Capture`.
- **Fallbacks.** Run `vo search "zzqqxx"`. The only section is `Use "zzqqxx" with…`.
- **Open app.** Pick an app that is already open, for example `Brave`. Run `vo windows-before`, `vo open "brave"`, and `vo key Return`. `vo new-windows` prints `[]` and the Brave window has focus (`hyprctl activewindow -j`).
- **Proof.** Keep `root-empty-crop.png` and the `vo search` output.

## Gotchas

- Never press Enter on a fallback row. It opens browser tabs.
- Starting an app that is not open creates a window. `vo clean` closes it only if `vo windows-before` ran first.
