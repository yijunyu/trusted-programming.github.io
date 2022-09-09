---
layout: post
title: Contributions to the Rust compiler
toc: true
---

# Const Generics 

```
Bastian Kauschke (lcnr)
Trusted Programming
Huawei Technologies, Inc. & LCNR
```

Const generics allows the use of values in the type system. Most often used for arrays with a generic size: `[u32; N]` where `N` can be an arbitrary usize. It improves code clarity, reusability and the general experience of working with arrays. This can reduce heap allocations and increase performance. Changes to the standard library relying on const generics also increased the compilation speed and documentation quality.

## Rationale
Const generics is part of [the Compiler Roadmap Expressiveness Aspirations](https://blog.rust-lang.org/inside-rust/2022/02/22/compiler-team-ambitions-2022.html#expressiveness-aspirations--).

In version 1.51 [an MVP for const generics](https://github.com/rust-lang/rust/pull/79135) has been stablized. This allows types to be parametric only over integers, `char` and `bool`. It however forbids computations in type system constants, only allowing generic parameters `const N: usize`, meaning "this can be any constant of type `usize`", and concrete values. Constants like `N + 1` are not allowed in the type system.

There are currently multiple unstable extensions to const generics which are already used by the ecosystem, even though they are still unstable.

## Areas

### [adt_const_params](https://github.com/rust-lang/rust/issues/95174)
```rust
feature(adt_const_params)
```
Allows more types as const parameters, most notably `&'static str`, arrays and slices, and user-defined types.

Working on this also requires some general improvements to pattern matching in Rust, most notably it requires us to clean up the situation wrt [structural match](https://github.com/rust-lang/rust/issues/74446). This by itself would already be a great improvement.

#### Examples
##### [luminance](https://crates.io/crates/luminance)
As explained in https://phaazon.net/blog/2022-luminance-redesign-part-1, they are using `const NAME: &'static str` on a trait to encode which fields are available in the type system. This moves a common source of runtime errors when writing shaders to compile time.

##### [Rust GPU](https://github.com/EmbarkStudios/rust-gpu)
Rust GPU uses an Image type which is generic over the kind of image. For that they [currently use 6 different const parameters of type u32](https://github.com/EmbarkStudios/rust-gpu/blob/a9a233eb80f6d5d512130f8c12469a1a74f58c65/crates/spirv-std/src/image.rs#L89-L108). As this is hard to understand, they provide a macro to refer to the different image options by name.

With `feature(adt_const_params)`, the following struct could instead be used, resulting in only 1 const parameter on Image:
```rust
struct ImageConfig {
    dim: u32,
    depth: u32,
    arrayed: u32,
    multisampled: u32,
    sampled: u32,
    format: u32,
}
```
This would remove the need for the `Image!` macro and improve error messages.

```rust
[T; N]: Default
```
The Default trait is [manually implemented for arrays up to size 32](https://github.com/rust-lang/rust/blob/ccb5595df2ed412eda6444edc7eaf06f709fa79d/library/core/src/array/mod.rs#L382-L405). This both prevents some useful code from compiling, has a small negative impact on compilation speed, and makes the documentation for the Default trait harder to read.

```rust
// This doesn't compile right now.
fn with_default<T: Default, const N: usize>() -> [T; N] {
    Default::default()
}
```
The reason that we still have manual implementations is that `[T; 0]` implements Default even if `T` does not implement `Default`.

Fixing in the near future is possible using some hacks which feels useful enough to try.

### [generic_arg_infer](https://github.com/rust-lang/rust/issues/85077)

```rust
feature(generic_arg_infer)
```
Allows for `_` as a const argument. While `[_; 3]` is an array of length 3 whose type should be inferred, `[u8; _]` should be an array whose length should be inferred. This feature enables that.

### [generic_const_exprs](https://github.com/rust-lang/rust/issues/76560)
```rust
feature(generic_const_exprs)
```
Allows for computations as arguments for const parameters.

```rust
fn split_first<T, const N: usize>(x: [T; N]) -> (T, [T; N - 1]) {
    todo!()
}

trait Encode {
    const LEN: usize;
    
    fn encode(&self) -> [u8; Self::LEN];
}
```
This is very desirable and useful feature but also a lot of complex issues we still have to solve. I do not intend to focus on this feature right now.
