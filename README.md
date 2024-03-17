## cargo-show

[![crates.io version](https://img.shields.io/crates/v/cargo-show.svg)](https://crates.io/crates/cargo-show)
[![Build status](https://github.com/g-k/cargo-show/actions/workflows/build.yml/badge.svg)](https://github.com/g-k/cargo-show/actions/workflows/build.yml)

Prints package metadata like pip show, apt-cache show, npm view, gem query, etc.

To install:

```sh
$ cargo install cargo-show
    Updating crates.io index
 Downloading crates ...
  Downloaded cargo-show v0.6.0
  Installing cargo-show v0.6.0
    Updating crates.io index
...
   Compiling g-k-crates-io-client v0.40.1
   Compiling cargo-show v0.6.0
    Finished release [optimized] target(s) in 11.41s
  Installing /Users/gguthe/.cargo/bin/cargo-show
   Installed package `cargo-show v0.6.0` (executable `cargo-show`)
$
```

Usage:

```sh
$ cargo show --help
Usage:
    cargo show [options] <crate-name>...
    cargo show (-h|--help)
    cargo show --version

Options:
    --json                  Print the JSON response.
    -L --dependencies       Print the crate's dependencies as well.
    -h --help               Show this help page.
    --version               Show version.

Display a metadata for a create at crates.io.
```

To print package metadata:

```sh
$ cargo show nonexistent-package servo
Error fetching data for nonexistent-package: the remote server responded with an error (status 404 Not Found): crate `nonexistent-package` does not exist
---
id: servo
name: servo
description: Parked non-servo thing
documentation: None
homepage: None
repository: None
max_version: 0.0.1
downloads: 7344
license: None
created: 2014-12-04T23:41:05.915728+00:00
updated: 2015-12-11T23:55:55.315022+00:00
```

To print JSON:

```json
$ cargo show --json serde | cut -b '1-120'
{"categories":[{"category":"No dynamic allocation","crates_cnt":329,"created_at":"2023-01-23T10:07:45.986892+00:00","des
```

To print package metadata and direct dependencies (alternatively use `-L`):

```sh
$ cargo show --dependencies time
---
id: time
name: time
description: Date and time library. Fully interoperable with the standard library. Mostly compatible with #![no_std].
documentation: None
homepage: https://time-rs.github.io
repository: https://github.com/time-rs/time
max_version: 0.3.34
downloads: 222936436
license: None
created: 2014-11-13T06:52:51.369245+00:00
updated: 2024-02-03T22:30:48.136812+00:00
dependencies:
deranged ^0.3.9
num-conv ^0.1.0
powerfmt ^0.2.0
time-core =0.1.2
itoa ^1.0.1 (opt)
js-sys ^0.3.58 (opt)
libc ^0.2.98 (opt)
num_threads ^0.1.2 (opt)
quickcheck ^1.0.3 (opt)
rand ^0.8.4 (opt)
serde ^1.0.184 (opt)
time-macros =0.2.17 (opt)
criterion ^0.5.1 (dev)
num-conv ^0.1.0 (dev)
quickcheck_macros ^1.0.0 (dev)
rand ^0.8.4 (dev)
rstest ^0.18.2 (dev)
rstest_reuse ^0.6.0 (dev)
serde ^1.0.184 (dev)
serde_json ^1.0.68 (dev)
serde_test ^1.0.126 (dev)
time-macros =0.2.17 (dev)
trybuild ^1.0.68 (dev)
```


To print package metadata and direct dependencies as JSON:

```sh
$ cargo show --dependencies --json time | python -m json.tool | head -n25
{
    "dependencies": [
        {
            "crate_id": "criterion",
            "default_features": false,
            "downloads": 0,
            "features": [],
            "id": 9234563,
            "kind": "dev",
            "optional": false,
            "req": "^0.5.1",
            "target": "cfg(bench)",
            "version_id": 1038365
        },
        {
            "crate_id": "deranged",
            "default_features": false,
            "downloads": 0,
            "features": [
                "powerfmt"
            ],
            "id": 9234543,
            "kind": "normal",
            "optional": false,
            "req": "^0.3.9",
```


To rename the command if you're used to other package managers:

```sh
$ cd /usr/local/bin/  # or someplace in path
$ ln $(which cargo-show) cargo-flizblorp  # needs to be a hardlink
$ cargo --list | grep fliz
    flizblorp
```

### Maintainers

* [@g-k](https://github.com/g-k)
* [@pravic](https://github.com/pravic)

### Contributors

* [@g-k](https://github.com/g-k)
* [@leoschwarz](https://github.com/leoschwarz)
* [@pravic](https://github.com/pravic)
