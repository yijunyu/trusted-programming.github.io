---
layout: post
title: Contributions to the Rust std library by Huawei Trusted Programming 
toc: true
---

# Standard Library support of Scoped Threads

```
Mara Bos
Trustworthiness Software Engineering & Open Source Lab
Huawei Technologies, Inc.
```

Here's an example usage of scoped threads:

```rust
fn main() {
    let config = read_config();

    let state = SharedAppState::new();

    thread::scope(|s| {
        // audio thread
        s.spawn(|| {
            // We can borrow local variables of `main` here,
            // because thread::scope guarantees the main function
            // will not stop before these threads stop.
            handle_audio(&config, &state);
        });

        // comm. thread
        s.spawn(|| {
            handle_comm(&config, &state);
        });

        // main thread: gui
        handle_gui(&config, &state);
    });
}
```

Without scoped threads, the config and state variables would have to be put in an Arc (reference-counted allocation), and the programmer would have to manually `.join()` the threads to make sure `main` doesn't end and exit the program too early. A thread scope makes this easier.

There are some more examples with a detailed explanation [here](https://rust-lang.github.io/rfcs/3151-scoped-threads.html#guide-level-explanation).

See also this [issue](https://rust-lang.github.io/rfcs/3151-scoped-threads.html#guide-level-explanation).
