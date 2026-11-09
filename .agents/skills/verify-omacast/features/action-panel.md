# Action panel

The action panel lists every action for the selected row with its shortcut. The About panel shows details of the selected row.

## Sub-features

- `actions-open` opens the panel with Ctrl+K and lists actions in groups.
- `actions-run` runs the selected action with Enter.
- `actions-about` opens the About panel with Ctrl+Shift+K.

## How to get to it (user POV)

- Select a row and press Ctrl+K.
- Select a row and press Ctrl+Shift+K.

## Driving it with vo

Preconditions:

- `vo doctor` shows no FAIL line.
- For file rows, `vo fixture` ran.

- **Open panel.** Run `vo open "zebrafish notes"` and `vo key ctrl+k`. Run `vo shot actions-file`. The crop lists Open File (↵), Show in Files (Ctrl ↵), and Copy Path (Ctrl Shift C).
- **Close panel.** Run `vo key Escape`. The panel closes and the launcher stays open.
- **About.** Run `vo key ctrl+shift+k` and `vo shot actions-about`. The crop shows Name, Where, and Modified for the file.
- **Proof.** Keep both crops.

## Gotchas

- Escape closes the panel first. A second Escape goes back or hides the launcher.
- The panel takes keys while it is open. Close it before you type a new query.
