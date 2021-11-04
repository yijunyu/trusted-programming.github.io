# FFI Unwind

```
Amanieu d'Antras
Principal Rust Expert
Trustworthy Open-Source Software Engineering Lab &
Ireland Research Centre
Huawei Technology, Inc.
```

## Goal
We introduce a new ABI string, `"C-unwind"`, to enable unwinding from other languages (such as C++) into Rust frames and from Rust into other languages. Additionally, we define the behavior for a limited number of previously-undefined cases when an unwind operation reaches a Rust function boundary with a non-`"Rust"`, non-`"C-unwind"` ABI.

As part of this specification, we introduce the term ["Plain Old Frame" (POF)](https://rust-lang.github.io/rfcs/2945-c-unwind-abi.html#plain-old-frames). These are frames that have no pending destructors and can be trivially deallocated. This RFC does not define the behavior of `catch_unwind` in a Rust frame being unwound by a foreign exception. This is something the [project group](https://github.com/rust-lang/project-ffi-unwind) would like to specify in a future RFC; as such, it is "TBD" (see ["Unresolved questions"](https://rust-lang.github.io/rfcs/2945-c-unwind-abi.html#unresolved-questions)).

Detailed descriptions see [2945-c-unwind-abi - The Rust RFC Book (rust-lang.github.io)](https://rust-lang.github.io/rfcs/2945-c-unwind-abi.html)

Progress see https://github.com/rust-lang/rust/issues/74990. 

```plantuml
collections Rust
collections "other languages such as C++" as Other
collections "plain old frames" as POF
alt
   Rust -> Other: ABI c_unwind
   Other -> Rust: c_unwind()\n non-Rust, non-unwind ABI
else
   Rust -> POF: POF without destructors
   POF -> Rust: POF without destructors 

end

```


## Updates

There are a number of pending issues to be done.

- [x] Will double check these dependencies to plan for the enhancements. 
- [ ] blocked by windows unwinding expertise 
- [ ] todo: help unblock it

