---
layout: post
title: Inline Assembler
---

# Inline Assembler

```
Amanieu d'Antras
Principal Rust Expert
Trustworthy Open-Source Software Engineering Lab &
Ireland Research Centre
Huawei Technology, Inc.
```
## Detailed descriptions see [Rust issue 72016](https://github.com/rust-lang/rust/issues/72016). 

Inline assemblers supports to get better performance, predictable clock cyclers, and accessible specialized hardware instructions. 

```plantuml
collections Rust
collections Assembler
collections Machine
collections Executable
alt
   Rust -> Assembler: A', B' = compile(A), compile(B)
   Assembler -> Machine: A'', B'' = assemble(A'), assemble(B')
else
   Rust -> Machine: AB' = inline(A, B')
end
Machine -> Executable: E = link(A'', B'', AB')
```

## Overall status

To be merged into stable in 3-4 months: some additional concerns for the blocking API features, so it may take a bit more time to become stable. 

## Update this week: 

- [x] The inline assembly request for change (RFC) has been merged and new implementation ready for experimentation;
- [x] Understood the scenarios of using inline assembler;
- [x] Resolved on blocking issue, response was positive;
- [x] Namespace decision to use without import (resolved); 
- [x] Two issues remaining before stablilization;
- [x] Got usage feedback from real users. 
- [x] To split the feature gates to partial stabilizing, which is to be stablizing by the language team: commiting to never change the API in the future
- [x] Finish documentation and has been stablised
- [x] Follow-up work for missing parts (stabilizing everything).
- [ ] Evaluate the usefulness with product lines 
