# Polymorphization

```
David Wood
Edinburgh Research Centre, UK
Huawei Technology, Inc.
```

**Goal**: Reduce binary size through polymorphism: https://rust-lang.github.io/compiler-team/working-groups/polymorphization/

Other ways to reduce binary size are listed [here](https://github.com/johnthagen/min-sized-rust).

- [x] Submitted #89426 (https://github.com/rust-lang/rust/pull/89426) which gets polymorphization to pass all of the tests on master, 
- [ ] [rust-lang/rust#75325] is the biggest remaining blocker for polymorphization. lcnr is working on a fix which should also enable greater polymorphization in the long run. Work-in-progress PR at [rust-lang/rust#90057](https://github.com/rust-lang/rust/pull/90057), and some rough sketches of the design [in a HackMD document](https://hackmd.io/CJ2zzXm0RtGORidx83RtBg). Will be reviewed by davidtwco.

