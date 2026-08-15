# raycast-snippets

Raycast snippet packs authored as markdown, converted to Raycast's import JSON.

Each pack lives in a single `<topic>.md` file with one section per snippet:

```markdown
## snippet name

`;keyword`

​```lang
snippet body with {cursor} placeholder
​```
```

`md2snippets.py` walks every `.md` beside it and emits a matching `<topic>.json`
in Raycast's import format.

## Packs

| Pack       | Snippets | Prefix    |
| ---------- | -------: | --------- |
| `bash.md`  |       34 | `;sh…`    |
| `marimo.md`|       37 | `;mo…`    |
| `mise.md`  |       30 | `;mise…`  |

## Usage

Build all JSON files:

```bash
mise run build      # or: python3 md2snippets.py
```

`build` uses mise's `sources`/`outputs` caching, so it only re-runs when a
`.md` or the script changes. `mise run clean` removes the generated JSON.

Live rebuild while editing:

```bash
mise watch -t build
```

Import into Raycast:

Raycast → Settings → Snippets → Import → pick a `.json` file.
