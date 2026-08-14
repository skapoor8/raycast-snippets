---
tags: [snippets, bash]
---

# bash

<!-- generated from bash.json by snippets2md.py — edit the JSON, not this file -->

34 snippets. Import via Raycast → Settings → Snippets → Import → `bash.json`.

| keyword | snippet |
| --- | --- |
| `;shstrict` | [[#strict mode header]] |
| `;shdir` | [[#script dir]] |
| `;shdie` | [[#die helper]] |
| `;shtrap` | [[#temp dir with cleanup trap]] |
| `;shrequire` | [[#require a command]] |
| `;shfunc` | [[#function with locals]] |
| `;shargs` | [[#arg parsing (long flags)]] |
| `;shgetopts` | [[#arg parsing (getopts, short flags)]] |
| `;shusage` | [[#usage heredoc]] |
| `;shreqargs` | [[#require positional args]] |
| `;shloopargs` | [[#loop over positional args]] |
| `;shfor` | [[#for over list]] |
| `;shforarr` | [[#for over array]] |
| `;shrange` | [[#for over range]] |
| `;shforc` | [[#for C-style]] |
| `;shforglob` | [[#for over files (glob)]] |
| `;shwhileread` | [[#while read lines from file]] |
| `;shwhilecmd` | [[#while read from command]] |
| `;shfind0` | [[#while read null-delimited (find)]] |
| `;shfields` | [[#while read fields]] |
| `;shuntil` | [[#until loop (retry)]] |
| `;shretry` | [[#retry with attempts]] |
| `;shif` | [[#if / elif / else]] |
| `;shstrtest` | [[#string tests]] |
| `;shnumtest` | [[#numeric tests]] |
| `;shfiletest` | [[#file tests]] |
| `;shcase` | [[#case statement]] |
| `;shregex` | [[#regex match]] |
| `;shdefault` | [[#default and required values]] |
| `;shguard` | [[#short-circuit guard]] |
| `;sharr` | [[#array]] |
| `;shmap` | [[#associative array]] |
| `;shstr` | [[#string manipulation]] |
| `;shheredoc` | [[#heredoc]] |

## strict mode header

`;shstrict`

```bash
#!/usr/bin/env bash
set -euo pipefail

{cursor}
```

## script dir

`;shdir`

```bash
script_dir="$(cd -- "$(dirname -- "${BASH_SOURCE[0]}")" && pwd)"
```

## die helper

`;shdie`

```bash
die() {
  printf 'error: %s\n' "$*" >&2
  exit 1
}
```

## temp dir with cleanup trap

`;shtrap`

```bash
tmp="$(mktemp -d)"
cleanup() { rm -rf "$tmp"; }
trap cleanup EXIT

{cursor}
```

## require a command

`;shrequire`

```bash
command -v {cursor} >/dev/null 2>&1 || die "{cursor} is required"
```

## function with locals

`;shfunc`

```bash
{cursor}() {
  local name="${1:?name required}"
  local greeting="${2:-hello}"

  printf '%s, %s!\n' "$greeting" "$name"
}
```

## arg parsing (long flags)

`;shargs`

```bash
usage() {
  cat <<'EOF'
Usage: script [options] <input>...

Options:
  -o, --out FILE   Write results to FILE
  -v, --verbose    Print more output
  -h, --help       Show this help
EOF
}

out=""
verbose=false
args=()

while [[ $# -gt 0 ]]; do
  case "$1" in
    -o | --out)
      [[ $# -ge 2 ]] || die "--out needs a value"
      out="$2"
      shift 2
      ;;
    -v | --verbose)
      verbose=true
      shift
      ;;
    -h | --help)
      usage
      exit 0
      ;;
    --)
      shift
      args+=("$@")
      break
      ;;
    -*)
      usage >&2
      die "unknown option: $1"
      ;;
    *)
      args+=("$1")
      shift
      ;;
  esac
done

set -- "${args[@]+"${args[@]}"}"
[[ $# -gt 0 ]] || { usage >&2; die "at least one input is required"; }

{cursor}
```

## arg parsing (getopts, short flags)

`;shgetopts`

```bash
out=""
verbose=false

while getopts ":o:vh" opt; do
  case "$opt" in
    o) out="$OPTARG" ;;
    v) verbose=true ;;
    h) usage; exit 0 ;;
    :) die "option -$OPTARG needs a value" ;;
    \?) die "unknown option: -$OPTARG" ;;
  esac
done
shift $((OPTIND - 1))

{cursor}
```

## usage heredoc

`;shusage`

```bash
usage() {
  cat <<'EOF'
Usage: {cursor} [options] <arg>

Options:
  -h, --help   Show this help
EOF
}
```

## require positional args

`;shreqargs`

```bash
[[ $# -ge {cursor} ]] || die "usage: $0 <arg>"
```

## loop over positional args

`;shloopargs`

```bash
for arg in "$@"; do
  {cursor}
done
```

## for over list

`;shfor`

```bash
for item in {cursor}; do
  printf '%s\n' "$item"
done
```

## for over array

`;shforarr`

```bash
for item in "${{cursor}[@]}"; do
  printf '%s\n' "$item"
done
```

## for over range

`;shrange`

```bash
for i in {1..{cursor}}; do
  printf '%s\n' "$i"
done
```

## for C-style

`;shforc`

```bash
for ((i = 0; i < {cursor}; i++)); do
  printf '%s\n' "$i"
done
```

## for over files (glob)

`;shforglob`

```bash
shopt -s nullglob
for file in {cursor}/*.txt; do
  printf '%s\n' "$file"
done
shopt -u nullglob
```

## while read lines from file

`;shwhileread`

```bash
while IFS= read -r line; do
  printf '%s\n' "$line"
done < "{cursor}"
```

## while read from command

`;shwhilecmd`

```bash
while IFS= read -r line; do
  printf '%s\n' "$line"
done < <({cursor})
```

## while read null-delimited (find)

`;shfind0`

```bash
while IFS= read -r -d '' file; do
  printf '%s\n' "$file"
done < <(find {cursor} -type f -print0)
```

## while read fields

`;shfields`

```bash
while IFS=, read -r first second rest; do
  printf '%s -> %s\n' "$first" "$second"
done < "{cursor}"
```

## until loop (retry)

`;shuntil`

```bash
until {cursor}; do
  sleep 1
done
```

## retry with attempts

`;shretry`

```bash
attempts=5
for ((i = 1; i <= attempts; i++)); do
  if {cursor}; then
    break
  fi
  [[ $i -lt $attempts ]] || die "failed after $attempts attempts"
  sleep $((i * 2))
done
```

## if / elif / else

`;shif`

```bash
if [[ {cursor} ]]; then
  :
elif [[ -n "$other" ]]; then
  :
else
  :
fi
```

## string tests

`;shstrtest`

```bash
[[ -z "${{cursor}:-}" ]] && echo "unset or empty"
[[ -n "${var:-}" ]] && echo "set"
[[ "$a" == "$b" ]] && echo "equal"
[[ "$a" != "$b" ]] && echo "different"
[[ "$name" == pre* ]] && echo "prefix match"
```

## numeric tests

`;shnumtest`

```bash
if (( {cursor} > 10 )); then
  echo "greater"
elif (( count == 0 )); then
  echo "zero"
fi
```

## file tests

`;shfiletest`

```bash
[[ -e "{cursor}" ]] || die "missing: $path"
[[ -f "$path" ]] && echo "regular file"
[[ -d "$path" ]] && echo "directory"
[[ -s "$path" ]] && echo "not empty"
[[ -r "$path" ]] && echo "readable"
[[ -x "$path" ]] && echo "executable"
```

## case statement

`;shcase`

```bash
case "${cursor}" in
  start)
    echo "starting"
    ;;
  stop | halt)
    echo "stopping"
    ;;
  *)
    die "usage: $0 {start|stop}"
    ;;
esac
```

## regex match

`;shregex`

```bash
if [[ "{cursor}" =~ ^([0-9]+)\.([0-9]+)\.([0-9]+)$ ]]; then
  major="${BASH_REMATCH[1]}"
  minor="${BASH_REMATCH[2]}"
  patch="${BASH_REMATCH[3]}"
fi
```

## default and required values

`;shdefault`

```bash
name="${1:-default}"
: "${{cursor}:?must be set}"
```

## short-circuit guard

`;shguard`

```bash
{cursor} || die "failed"
```

## array

`;sharr`

```bash
items=({cursor})
items+=("another")

printf '%s\n' "${items[@]}"
echo "count: ${#items[@]}"
echo "first: ${items[0]}"
```

## associative array

`;shmap`

```bash
# bash 4+; on bash 3.2 (macOS /bin/bash) this silently becomes an indexed array
declare -A {cursor}=([host]=localhost [port]=8080)
config[user]=admin

for key in "${!config[@]}"; do
  printf '%s=%s\n' "$key" "${config[$key]}"
done
```

## string manipulation

`;shstr`

```bash
path="{cursor}/report.tar.gz"

echo "${path##*/}"        # report.tar.gz  — basename
echo "${path%/*}"         # leading dirs   — dirname
echo "${path%%.*}"        # strip all extensions
echo "${path//old/new}"   # replace every match
echo "${path^^}"          # upper case (bash 4+)
echo "${#path}"           # length
```

## heredoc

`;shheredoc`

```bash
cat <<'EOF'
literal text, $no expansion
EOF

cat <<EOF
expanded: ${cursor}
EOF
```
