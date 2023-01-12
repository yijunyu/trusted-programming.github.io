---
layout: post
title: Txl wrapper for Rust
toc: true
---

```
Yijun Yu
Trusted Programming
Huawei Technology Inc.
```

[Repo](https://github.com/trusted-programming/txl-rs)

# Txl wrapper for Rust

[`txl`](http://txl.ca) is a transformation system developed by James R. Cordy
at Queen's University. This crate provides a cross-platform command line utility to install it,
while offering a convenient function to invoke it inside Rust code.

## Installation

Install the command:
```bash
cargo install txl-rs
```

Install the library:
```toml
[dependencies]
txl-rs = "0.0.3"
```

## Usage

### Command line usage
```bash
txl-rs [args]
```
which would run as if it is a `txl [args]` command.

### Library usage
```rust
use txl_rs::txl;

fn main() {
    match txl(["src/main.rs"]) {
        Ok(result) => {
            println!("{result}");
        }
        Err(error) => {
            println!("{error}");
        }
    }
}
```

## Acknowledgement

## Updates
- [x] Integrate with Rust
- [x] make it platform independent
- [x] Publish the crate
- [x] adaptively downlad relevant parser packages 
- [ ] implement transformations as clippy fix rules

## Acknowledgement
* Thanks Prof. James R. Cordy from Queen's University for the excellent work on [TXL](http://txl.ca). 
