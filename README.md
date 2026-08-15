# raycast-snippets

Raycast snippet packs authored as markdown, converted to Raycast's import JSON.

Each pack lives in a single `<topic>.md` file with one section per snippet:

```markdown
## snippet name

`;keyword`

```lang
snippet body with {cursor} placeholder
```
```

`md2snippets.py` walks every `.md` beside it and emits a matching `<topic>.json`
in Raycast's import format.

## Packs

| Pack       | Snippets | Prefix    |
| ---------- | -------: | --------- |
| `bash.md`  |       34 | `;sh…`    |
| `marimo.md`|       37 | `;mo…`    |
| `mise.md`  |       30 | `;mise…`  |

## Installation

Install a pack by importing its JSON into Raycast:

1. Build the JSON files:

   ```bash
   mise run build      # or: python3 md2snippets.py
   ```

2. Import a pack:

   Raycast → Settings → Snippets → Import → pick a `<topic>.json` file.

Repeat for each pack you want. Re-import a pack later to pick up snippet updates.

## Usage

With a pack imported, type a snippet's `;keyword` in any Raycast text field
(search bar, chat, form, …) and Raycast replaces it with the snippet body,
placing the cursor where the `{cursor}` placeholder was.

For example, after importing `bash.md`, type `;shstrict` to expand the "strict
mode header" snippet.

## Maintenance

Snippets are maintained and updated via the **snippets skill** from
`github:cloudvoyant/codevoyant`. The `.md` files in this repo are the source of
truth; the skill generates the Raycast snippets from them.

- add a snippet: `snippets add "<snippet>"`
- update a snippet: `snippets update <name>`
- rebuild all JSON from markdown: `snippets update`

`mise run build` performs the same `.md` → `.json` conversion locally
(`python3 md2snippets.py`), and `mise run clean` removes the generated JSON.

Live rebuild while editing:

```bash
mise watch -t build
```
