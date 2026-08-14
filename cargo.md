---
tags: [snippets, cargo, rust]
---

# cargo

<!-- generated from cargo.json by snippets2md.py — edit the JSON, not this file -->

28 snippets. Import via Raycast → Settings → Snippets → Import → `cargo.json`.

| keyword | snippet |
| --- | --- |
| `;cgbin` | [[#binary crate Cargo.toml]] |
| `;cglib` | [[#library crate Cargo.toml]] |
| `;cgws` | [[#workspace root Cargo.toml]] |
| `;cgmember` | [[#workspace member Cargo.toml]] |
| `;cgpkg` | [[#[package] block]] |
| `;cgdeps` | [[#[dependencies] starter]] |
| `;cgdev` | [[#[dev-dependencies]]] |
| `;cgbuild` | [[#[build-dependencies]]] |
| `;cgfeat` | [[#[features]]] |
| `;cgbin2` | [[#additional [[bin]] entry]] |
| `;cglibsec` | [[#[lib] section]] |
| `;cgex` | [[#[[example]] entry]] |
| `;cgbench` | [[#[[bench]] entry]] |
| `;cgtest` | [[#[[test]] integration entry]] |
| `;cgprofrel` | [[#[profile.release] optimized]] |
| `;cgprofdev` | [[#[profile.dev] fast compile]] |
| `;cgpatch` | [[#[patch.crates-io]]] |
| `;cgwsdeps` | [[#[workspace.dependencies]]] |
| `;cgwspkg` | [[#[workspace.package]]] |
| `;cgwslints` | [[#[workspace.lints]]] |
| `;cglints` | [[#[lints] inherit from workspace]] |
| `;cgserde` | [[#serde dep]] |
| `;cgtokio` | [[#tokio dep]] |
| `;cgtracing` | [[#tracing deps]] |
| `;cgpath` | [[#path dep (workspace member)]] |
| `;cggit` | [[#git dep]] |
| `;cgopt` | [[#optional dep behind feature]] |
| `;cginherit` | [[#dep inherited from workspace]] |

## binary crate Cargo.toml

`;cgbin`

```toml
[package]
name = "{cursor}"
version = "0.1.0"
edition = "2024"
description = ""
license = "MIT OR Apache-2.0"

[dependencies]
anyhow = "1"
```

## library crate Cargo.toml

`;cglib`

```toml
[package]
name = "{cursor}"
version = "0.1.0"
edition = "2024"
description = ""
license = "MIT OR Apache-2.0"
repository = ""

[lib]
name = "{cursor}"
path = "src/lib.rs"

[dependencies]
thiserror = "2"

[dev-dependencies]
pretty_assertions = "1"
```

## workspace root Cargo.toml

`;cgws`

```toml
[workspace]
resolver = "2"
members = ["crates/*"]
default-members = ["crates/{cursor}"]

[workspace.package]
version = "0.1.0"
edition = "2024"
authors = ["{cursor}"]
license = "MIT OR Apache-2.0"
repository = ""

[workspace.dependencies]
anyhow = "1"
thiserror = "2"
serde = { version = "1", features = ["derive"] }
serde_json = "1"
tokio = { version = "1", features = ["full"] }
tracing = "0.1"
tracing-subscriber = { version = "0.3", features = ["env-filter"] }

[workspace.lints.rust]
unsafe_code = "forbid"

[workspace.lints.clippy]
pedantic = { level = "warn", priority = -1 }
nursery = { level = "warn", priority = -1 }

[profile.release]
lto = "thin"
codegen-units = 1
strip = true
```

## workspace member Cargo.toml

`;cgmember`

```toml
[package]
name = "{cursor}"
version.workspace = true
edition.workspace = true
authors.workspace = true
license.workspace = true
repository.workspace = true

[dependencies]
anyhow.workspace = true
thiserror.workspace = true
serde.workspace = true

[lints]
workspace = true
```

## [package] block

`;cgpkg`

```toml
[package]
name = "{cursor}"
version = "0.1.0"
edition = "2024"
description = ""
license = "MIT OR Apache-2.0"
repository = ""
readme = "README.md"
keywords = []
categories = []
```

## [dependencies] starter

`;cgdeps`

```toml
[dependencies]
anyhow = "1"
thiserror = "2"
serde = { version = "1", features = ["derive"] }
serde_json = "1"
tracing = "0.1"
{cursor}
```

## [dev-dependencies]

`;cgdev`

```toml
[dev-dependencies]
pretty_assertions = "1"
proptest = "1"
tempfile = "3"
{cursor}
```

## [build-dependencies]

`;cgbuild`

```toml
[build-dependencies]
{cursor}
```

## [features]

`;cgfeat`

```toml
[features]
default = ["{cursor}"]
{cursor} = []
```

## additional [[bin]] entry

`;cgbin2`

```toml
[[bin]]
name = "{cursor}"
path = "src/bin/{cursor}.rs"
```

## [lib] section

`;cglibsec`

```toml
[lib]
name = "{cursor}"
path = "src/lib.rs"
crate-type = ["rlib"]
```

## [[example]] entry

`;cgex`

```toml
[[example]]
name = "{cursor}"
path = "examples/{cursor}.rs"
```

## [[bench]] entry

`;cgbench`

```toml
[[bench]]
name = "{cursor}"
harness = false
```

## [[test]] integration entry

`;cgtest`

```toml
[[test]]
name = "{cursor}"
path = "tests/{cursor}.rs"
```

## [profile.release] optimized

`;cgprofrel`

```toml
[profile.release]
lto = "thin"
codegen-units = 1
strip = true
panic = "abort"
```

## [profile.dev] fast compile

`;cgprofdev`

```toml
[profile.dev]
opt-level = 0
debug = "line-tables-only"
incremental = true
```

## [patch.crates-io]

`;cgpatch`

```toml
[patch.crates-io]
{cursor} = { git = "https://github.com/", branch = "main" }
```

## [workspace.dependencies]

`;cgwsdeps`

```toml
[workspace.dependencies]
anyhow = "1"
thiserror = "2"
serde = { version = "1", features = ["derive"] }
serde_json = "1"
tokio = { version = "1", features = ["full"] }
tracing = "0.1"
tracing-subscriber = { version = "0.3", features = ["env-filter"] }
{cursor}
```

## [workspace.package]

`;cgwspkg`

```toml
[workspace.package]
version = "0.1.0"
edition = "2024"
authors = ["{cursor}"]
license = "MIT OR Apache-2.0"
repository = ""
```

## [workspace.lints]

`;cgwslints`

```toml
[workspace.lints.rust]
unsafe_code = "forbid"
missing_docs = "warn"

[workspace.lints.clippy]
pedantic = { level = "warn", priority = -1 }
nursery = { level = "warn", priority = -1 }
```

## [lints] inherit from workspace

`;cglints`

```toml
[lints]
workspace = true
```

## serde dep

`;cgserde`

```toml
serde = { version = "1", features = ["derive"] }
serde_json = "1"
```

## tokio dep

`;cgtokio`

```toml
tokio = { version = "1", features = ["full"] }
```

## tracing deps

`;cgtracing`

```toml
tracing = "0.1"
tracing-subscriber = { version = "0.3", features = ["env-filter"] }
```

## path dep (workspace member)

`;cgpath`

```toml
{cursor} = { path = "../{cursor}" }
```

## git dep

`;cggit`

```toml
{cursor} = { git = "https://github.com/", branch = "main" }
```

## optional dep behind feature

`;cgopt`

```toml
[dependencies]
{cursor} = { version = "1", optional = true }

[features]
{cursor} = ["dep:{cursor}"]
```

## dep inherited from workspace

`;cginherit`

```toml
{cursor}.workspace = true
```
