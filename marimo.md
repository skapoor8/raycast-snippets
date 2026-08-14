---
tags: [snippets, marimo]
---

# marimo

<!-- generated from marimo.json by snippets2md.py — edit the JSON, not this file -->

37 snippets. Import via Raycast → Settings → Snippets → Import → `marimo.json`.

| keyword | snippet |
| --- | --- |
| `;moimp` | [[#import]] |
| `;moapp` | [[#notebook skeleton]] |
| `;mopycell` | [[#python cell]] |
| `;momdcell` | [[#markdown cell]] |
| `;momd` | [[#markdown block]] |
| `;mohstack` | [[#hstack]] |
| `;movstack` | [[#vstack]] |
| `;motabs` | [[#tabs]] |
| `;moaccordion` | [[#accordion]] |
| `;mocallout` | [[#callout]] |
| `;moslider` | [[#ui.slider]] |
| `;monum` | [[#ui.number]] |
| `;motext` | [[#ui.text]] |
| `;modrop` | [[#ui.dropdown]] |
| `;momulti` | [[#ui.multiselect]] |
| `;mocheck` | [[#ui.checkbox]] |
| `;moradio` | [[#ui.radio]] |
| `;modate` | [[#ui.date]] |
| `;mofile` | [[#ui.file upload]] |
| `;motable` | [[#ui.table]] |
| `;modf` | [[#ui.dataframe explorer]] |
| `;morun` | [[#run button + stop guard]] |
| `;moform` | [[#form (defer reactivity)]] |
| `;mostop` | [[#stop]] |
| `;mostate` | [[#state]] |
| `;mosql` | [[#sql cell]] |
| `;moprogress` | [[#progress bar]] |
| `;mospinner` | [[#spinner]] |
| `;moalt` | [[#altair chart]] |
| `;mompl` | [[#interactive matplotlib]] |
| `;modl` | [[#download button]] |
| `;monbdir` | [[#notebook-relative path]] |
| `;mocli` | [[#cli args]] |
| `;moedit` | [[#edit in uv sandbox]] |
| `;morunapp` | [[#run as app]] |
| `;moconvert` | [[#convert from jupyter]] |
| `;moexport` | [[#export wasm site]] |

## import

`;moimp`

```python
import marimo as mo
```

## notebook skeleton

`;moapp`

```python
# /// script
# requires-python = ">=3.12"
# dependencies = [
#     "marimo",
# ]
# ///

import marimo

app = marimo.App(width="medium")


@app.cell
def _():
    import marimo as mo
    return (mo,)


@app.cell(hide_code=True)
def _(mo):
    mo.md(r"""# {cursor}""")
    return


@app.cell
def _(mo):
    pass
    return


if __name__ == "__main__":
    app.run()
```

## python cell

`;mopycell`

```python
@app.cell
def _(mo):
    {cursor}
    return
```

## markdown cell

`;momdcell`

```python
@app.cell(hide_code=True)
def _(mo):
    mo.md(
        r"""
        {cursor}
        """
    )
    return
```

## markdown block

`;momd`

```python
mo.md(
    f"""
    {cursor}
    """
)
```

## hstack

`;mohstack`

```python
mo.hstack([{cursor}], justify="start")
```

## vstack

`;movstack`

```python
mo.vstack([{cursor}])
```

## tabs

`;motabs`

```python
mo.tabs(
    {
        "Overview": {cursor},
        "Detail": second,
    }
)
```

## accordion

`;moaccordion`

```python
mo.accordion({"Details": {cursor}})
```

## callout

`;mocallout`

```python
mo.callout(mo.md("{cursor}"), kind="warn")
```

## ui.slider

`;moslider`

```python
n = mo.ui.slider(start=1, stop=100, step=1, value=10, label="{cursor}")
```

## ui.number

`;monum`

```python
n = mo.ui.number(start=0, stop=100, value=1, label="{cursor}")
```

## ui.text

`;motext`

```python
name = mo.ui.text(placeholder="{cursor}", label="name")
```

## ui.dropdown

`;modrop`

```python
choice = mo.ui.dropdown(options=["a", "b"], value="a", label="{cursor}")
```

## ui.multiselect

`;momulti`

```python
choices = mo.ui.multiselect(options=["a", "b"], label="{cursor}")
```

## ui.checkbox

`;mocheck`

```python
flag = mo.ui.checkbox(value=False, label="{cursor}")
```

## ui.radio

`;moradio`

```python
mode = mo.ui.radio(options=["a", "b"], value="a", label="{cursor}")
```

## ui.date

`;modate`

```python
day = mo.ui.date(label="{cursor}")
```

## ui.file upload

`;mofile`

```python
upload = mo.ui.file(filetypes=[".csv"], kind="area", label="{cursor}")
```

## ui.table

`;motable`

```python
tbl = mo.ui.table({cursor}, selection="multi", page_size=25)
```

## ui.dataframe explorer

`;modf`

```python
explorer = mo.ui.dataframe({cursor})
```

## run button + stop guard

`;morun`

```python
run = mo.ui.run_button(label="Run")
run

# downstream cell:
mo.stop(not run.value, mo.md("Click **Run** to continue."))
{cursor}
```

## form (defer reactivity)

`;moform`

```python
form = {cursor}.form(label="Submit")
```

## stop

`;mostop`

```python
mo.stop({cursor}, mo.md("Waiting for input."))
```

## state

`;mostate`

```python
get_count, set_count = mo.state({cursor})
```

## sql cell

`;mosql`

```python
result = mo.sql(
    f"""
    SELECT *
    FROM {cursor}
    """
)
```

## progress bar

`;moprogress`

```python
for item in mo.status.progress_bar(items, title="Working"):
    {cursor}
```

## spinner

`;mospinner`

```python
with mo.status.spinner(title="Loading..."):
    {cursor}
```

## altair chart

`;moalt`

```python
chart = mo.ui.altair_chart({cursor})
```

## interactive matplotlib

`;mompl`

```python
mo.mpl.interactive({cursor})
```

## download button

`;modl`

```python
mo.download(data={cursor}, filename="out.csv", label="Download")
```

## notebook-relative path

`;monbdir`

```python
mo.notebook_dir() / "{cursor}"
```

## cli args

`;mocli`

```python
args = mo.cli_args()
```

## edit in uv sandbox

`;moedit`

```bash
uv run --with marimo marimo edit {cursor} --sandbox
```

## run as app

`;morunapp`

```bash
marimo run {cursor}
```

## convert from jupyter

`;moconvert`

```bash
marimo convert {cursor}.ipynb > nb.py
```

## export wasm site

`;moexport`

```bash
marimo export html-wasm {cursor} -o site/
```
