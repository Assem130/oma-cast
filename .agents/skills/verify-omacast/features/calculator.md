# Calculator

The calculator shows an answer card above Results when the query is a calculation. Enter copies the answer.

## Sub-features

- `calc-card` shows the question, the answer, and a caption for each.
- `calc-copy` copies the answer with Enter and saves it to Calculator History.
- `calc-none` shows no card for a plain word or number.

## How to get to it (user POV)

- Press Ctrl+Space and type a calculation, for example `5 ft to cm`.

## Driving it with vo

Preconditions:

- `vo doctor` shows no FAIL line.

- **Card.** Run `vo open "12 * 12"` and `vo shot calc-card`. The crop shows a card with `12 * 12` and `144`.
- **Copy.** Run `vo key Return`. The launcher closes. `wl-paste` prints `144`.
- **None.** Run `vo search "firefox"`. No Calculator section.
- **Proof.** Keep `calc-card-crop.png` and the `wl-paste` output.

## Gotchas

- Enter on the card overwrites the clipboard. Tell the user if the run changes their clipboard.
- Currency answers need cached exchange rates. They can be missing offline.
