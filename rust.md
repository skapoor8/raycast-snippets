---
tags: [snippets, rust]
---

# rust

<!-- generated from rust.json by snippets2md.py — edit the JSON, not this file -->

43 snippets. Import via Raycast → Settings → Snippets → Import → `rust.json`.

| keyword | snippet |
| --- | --- |
| `;rsmain` | [[#main returning Result]] |
| `;rsmainsimple` | [[#main (simple)]] |
| `;rsmod` | [[#module declaration]] |
| `;rsfn` | [[#function]] |
| `;rsderive` | [[#struct with derives]] |
| `;rsnew` | [[#impl with new()]] |
| `;rsnewtype` | [[#newtype wrapper]] |
| `;rsenum` | [[#enum]] |
| `;rsdisplay` | [[#Display impl]] |
| `;rsfrom` | [[#From impl]] |
| `;rstrait` | [[#trait definition]] |
| `;rsimpltrait` | [[#impl trait for type]] |
| `;rserror` | [[#custom error (thiserror)]] |
| `;rsanyhow` | [[#anyhow context]] |
| `;rsresult` | [[#Result type alias]] |
| `;rsmatchopt` | [[#match Option]] |
| `;rsmatchres` | [[#match Result]] |
| `;rsiflet` | [[#if let]] |
| `;rsletelse` | [[#let else]] |
| `;rswhilelet` | [[#while let]] |
| `;rsfor` | [[#for loop]] |
| `;rsiter` | [[#iter map filter collect]] |
| `;rsfold` | [[#iter fold]] |
| `;rshm` | [[#HashMap literal]] |
| `;rshmentry` | [[#HashMap entry]] |
| `;rshs` | [[#HashSet literal]] |
| `;rsarc` | [[#Arc<Mutex<T>>]] |
| `;rsoncelock` | [[#OnceLock lazy static]] |
| `;rslifetime` | [[#function with lifetime]] |
| `;rsgeneric` | [[#generic function with where]] |
| `;rstest` | [[#test module]] |
| `;rstokio` | [[#tokio main]] |
| `;rsspawn` | [[#tokio spawn + join]] |
| `;rsclap` | [[#clap derive CLI]] |
| `;rsclapsub` | [[#clap subcommands]] |
| `;rsread` | [[#read file to string]] |
| `;rsdoccrate` | [[#crate doc comment]] |
| `;rsdocmod` | [[#module doc comment]] |
| `;rsdocfn` | [[#function doc comment]] |
| `;rsdocfull` | [[#doc comment with sections]] |
| `;rsdocex` | [[#doc example (doctest)]] |
| `;rsdocstruct` | [[#struct + field doc comments]] |
| `;rsdocsafety` | [[#safety doc comment]] |

## main returning Result

`;rsmain`

```rust
use std::error::Error;

fn main() -> Result<(), Box<dyn Error>> {
    {cursor}
    Ok(())
}
```

## main (simple)

`;rsmainsimple`

```rust
fn main() {
    {cursor}
}
```

## module declaration

`;rsmod`

```rust
mod {cursor};

pub use {cursor}::*;
```

## function

`;rsfn`

```rust
fn {cursor}(name: &str) -> String {
    format!("hello, {name}")
}
```

## struct with derives

`;rsderive`

```rust
#[derive(Debug, Clone, PartialEq, Eq, Hash)]
pub struct {cursor} {
    pub name: String,
    pub count: usize,
}
```

## impl with new()

`;rsnew`

```rust
impl {cursor} {
    pub fn new(name: impl Into<String>) -> Self {
        Self {
            name: name.into(),
            count: 0,
        }
    }
}
```

## newtype wrapper

`;rsnewtype`

```rust
#[derive(Debug, Clone, Copy, PartialEq, Eq, Hash)]
pub struct {cursor}(pub u64);

impl {cursor} {
    pub fn get(self) -> u64 {
        self.0
    }
}
```

## enum

`;rsenum`

```rust
#[derive(Debug, Clone, PartialEq, Eq)]
pub enum {cursor} {
    Empty,
    One(String),
    Many { items: Vec<String>, total: usize },
}
```

## Display impl

`;rsdisplay`

```rust
use std::fmt;

impl fmt::Display for {cursor} {
    fn fmt(&self, f: &mut fmt::Formatter<'_>) -> fmt::Result {
        write!(f, "{}", self.name)
    }
}
```

## From impl

`;rsfrom`

```rust
impl From<{cursor}> for String {
    fn from(value: {cursor}) -> Self {
        value.name
    }
}
```

## trait definition

`;rstrait`

```rust
pub trait {cursor} {
    fn name(&self) -> &str;

    fn describe(&self) -> String {
        format!("<{}>", self.name())
    }
}
```

## impl trait for type

`;rsimpltrait`

```rust
impl {cursor} for {cursor} {
    fn name(&self) -> &str {
        &self.name
    }
}
```

## custom error (thiserror)

`;rserror`

```rust
use thiserror::Error;

#[derive(Debug, Error)]
pub enum {cursor}Error {
    #[error("not found: {0}")]
    NotFound(String),

    #[error("invalid input: {reason}")]
    Invalid { reason: String },

    #[error(transparent)]
    Io(#[from] std::io::Error),
}

pub type Result<T> = std::result::Result<T, {cursor}Error>;
```

## anyhow context

`;rsanyhow`

```rust
use anyhow::{Context, Result};

fn {cursor}(path: &std::path::Path) -> Result<String> {
    std::fs::read_to_string(path)
        .with_context(|| format!("failed to read {}", path.display()))
}
```

## Result type alias

`;rsresult`

```rust
pub type Result<T, E = Box<dyn std::error::Error + Send + Sync>> = std::result::Result<T, E>;
```

## match Option

`;rsmatchopt`

```rust
match {cursor} {
    Some(value) => {
        println!("got {value}");
    }
    None => {
        println!("nothing");
    }
}
```

## match Result

`;rsmatchres`

```rust
match {cursor} {
    Ok(value) => {
        println!("ok: {value}");
    }
    Err(e) => {
        eprintln!("error: {e}");
    }
}
```

## if let

`;rsiflet`

```rust
if let Some({cursor}) = value {
    
}
```

## let else

`;rsletelse`

```rust
let Some({cursor}) = value else {
    return;
};
```

## while let

`;rswhilelet`

```rust
while let Some({cursor}) = iter.next() {
    
}
```

## for loop

`;rsfor`

```rust
for {cursor} in items {
    
}
```

## iter map filter collect

`;rsiter`

```rust
let {cursor}: Vec<_> = items
    .iter()
    .filter(|x| x.is_active)
    .map(|x| x.name.clone())
    .collect();
```

## iter fold

`;rsfold`

```rust
let total = items.iter().fold(0, |acc, x| acc + x.count);
```

## HashMap literal

`;rshm`

```rust
use std::collections::HashMap;

let {cursor}: HashMap<&str, i32> = HashMap::from([
    ("one", 1),
    ("two", 2),
    ("three", 3),
]);
```

## HashMap entry

`;rshmentry`

```rust
*counts.entry({cursor}).or_insert(0) += 1;
```

## HashSet literal

`;rshs`

```rust
use std::collections::HashSet;

let {cursor}: HashSet<&str> = HashSet::from(["a", "b", "c"]);
```

## Arc<Mutex<T>>

`;rsarc`

```rust
use std::sync::{Arc, Mutex};

let {cursor} = Arc::new(Mutex::new(Vec::<String>::new()));

{
    let handle = Arc::clone(&{cursor});
    std::thread::spawn(move || {
        handle.lock().unwrap().push("hello".into());
    });
}
```

## OnceLock lazy static

`;rsoncelock`

```rust
use std::sync::OnceLock;

fn {cursor}() -> &'static Vec<String> {
    static VALUE: OnceLock<Vec<String>> = OnceLock::new();
    VALUE.get_or_init(|| vec!["one".into(), "two".into()])
}
```

## function with lifetime

`;rslifetime`

```rust
fn {cursor}<'a>(input: &'a str, sep: &str) -> Vec<&'a str> {
    input.split(sep).collect()
}
```

## generic function with where

`;rsgeneric`

```rust
fn {cursor}<T>(items: &[T]) -> Option<&T>
where
    T: Ord,
{
    items.iter().max()
}
```

## test module

`;rstest`

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn {cursor}() {
        assert_eq!(2 + 2, 4);
    }
}
```

## tokio main

`;rstokio`

```rust
#[tokio::main]
async fn main() -> anyhow::Result<()> {
    {cursor}
    Ok(())
}
```

## tokio spawn + join

`;rsspawn`

```rust
let a = tokio::spawn(async {
    {cursor}
});
let b = tokio::spawn(async {
    
});

let (a, b) = tokio::try_join!(a, b)?;
```

## clap derive CLI

`;rsclap`

```rust
use clap::Parser;

#[derive(Debug, Parser)]
#[command(version, about)]
struct Cli {
    /// Input file
    input: std::path::PathBuf,

    /// Write output here
    #[arg(short, long)]
    out: Option<std::path::PathBuf>,

    /// Print more output
    #[arg(short, long)]
    verbose: bool,
}

fn main() -> anyhow::Result<()> {
    let cli = Cli::parse();
    {cursor}
    Ok(())
}
```

## clap subcommands

`;rsclapsub`

```rust
use clap::{Parser, Subcommand};

#[derive(Debug, Parser)]
#[command(version, about)]
struct Cli {
    #[command(subcommand)]
    command: Command,
}

#[derive(Debug, Subcommand)]
enum Command {
    /// Add a new item
    Add {
        /// Name of the item
        name: String,
    },
    /// Remove an item
    Remove {
        /// Name of the item
        name: String,

        /// Remove without confirming
        #[arg(short, long)]
        force: bool,
    },
    /// List all items
    List,
}

fn main() -> anyhow::Result<()> {
    let cli = Cli::parse();

    match cli.command {
        Command::Add { name } => {
            {cursor}
        }
        Command::Remove { name, force } => {}
        Command::List => {}
    }

    Ok(())
}
```

## read file to string

`;rsread`

```rust
let {cursor} = std::fs::read_to_string(path)?;
```

## crate doc comment

`;rsdoccrate`

```rust
//! # {cursor}
//!
//! One-line summary of what this crate does.
//!
//! More detail about the crate's purpose, the main entry points,
//! and how the pieces fit together.
//!
//! # Examples
//!
//! ```
//! use my_crate::run;
//!
//! run();
//! ```
```

## module doc comment

`;rsdocmod`

```rust
//! {cursor}
//!
//! Longer explanation of what this module provides and when to
//! reach for it.
```

## function doc comment

`;rsdocfn`

```rust
/// {cursor}
///
/// # Examples
///
/// ```
/// let result = add(2, 2);
/// assert_eq!(result, 4);
/// ```
```

## doc comment with sections

`;rsdocfull`

```rust
/// {cursor}
///
/// # Errors
///
/// Returns [`Err`] if the input cannot be parsed.
///
/// # Panics
///
/// Panics if the internal invariant is violated.
///
/// # Examples
///
/// ```
/// # use my_crate::parse;
/// let value = parse("42")?;
/// assert_eq!(value, 42);
/// # Ok::<(), std::num::ParseIntError>(())
/// ```
```

## doc example (doctest)

`;rsdocex`

```rust
/// # Examples
///
/// ```
/// # use my_crate::*;
/// let {cursor} = build();
/// assert!({cursor}.is_valid());
/// ```
```

## struct + field doc comments

`;rsdocstruct`

```rust
/// {cursor}
///
/// Describe the invariants callers can rely on.
pub struct Config {
    /// Human-readable name.
    pub name: String,
    /// Maximum number of retries before giving up.
    pub retries: usize,
}
```

## safety doc comment

`;rsdocsafety`

```rust
/// {cursor}
///
/// # Safety
///
/// The caller must ensure that `ptr` is non-null, properly aligned,
/// and valid for reads of `len` elements.
pub unsafe fn from_raw(ptr: *const u8, len: usize) {
    
}
```
