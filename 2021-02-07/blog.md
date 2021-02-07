# Our Rust Mission at Huawei

*Yijun Yu*

Chief Expert on Trusted Programming\
Trustworthy Open-Source Software Engineering Lab\
Huawei Technology, Inc.

*Amanieu d'Antras*

Principal Rust Expert\
Trustworthy Open-Source Software Engineering Lab\
Huawei Technology, Inc.

## Innovations by Rust

Since 2015, Rust has consistently been voted as the most loved
programming language in the StackOverflow survey.

![](img/RustConChina2020-yu-v42.png){width=500px}\

There has also been an increasing number of publications on Rust at recent top
programming languages and software engineering conferences. 

![](img/RustConChina2020-yu-v43.png)\

If that's not enough, a recent Nature 2020 article, `Why Scientists are Turning
to Rust', says that there is increasing momentum on the adoption of Rust
amongst scientists.

![](img/RustConChina2020-yu-v41.png){width=500px}\

## Initial adoption of Rust at Huawei 

At Huawei, we aim to engineer trustworthy software systems in the
world's largest telecom industry. 

For example, we are working to migrate parts of our code base towards
Rust, which is safer and as performant as C/C++. To assist our
developers in this process, we are leveraging the open-source
[C2Rust](https://c2rust.com/) transpiler to generate Rust code directly
from C. We have created automated tools to refactor and clean up this
generated Rust code through source-to-source transformations.

We also contribute significant features back to the Rust community. For
example, our recent contributions to the Rust compiler enable the
compilation of Rust programs for big-endian and
[ILP32](https://developer.arm.com/documentation/dai0490/latest/)
variants of AArch64.  These changes enable Huawei and other hardware
companies to run Rust code on networking hardware which commonly use
these architecture variants.  This contribution is achieved with the
help of our Rust expert Amanieu d'Antras, who has pushed through these
pull requests to [the LLVM
compiler](https://reviews.llvm.org/rG21bfd068b32ece1c6fbc912208e7cd1782a8c3fc),
[the libc crate](https://github.com/rust-lang/libc/pull/2039), and [the
Rust compiler itself](https://github.com/rust-lang/rust/pull/81455).
These changes introduce new end-to-end cross-compilation targets for the
Rust compiler, making it easier to build Rust products for bespoke
hardware using a single command:
```bash
cargo build --target aarch64_be-unknown-linux-gnu
cargo build --target aarch64-unknown-linux-gnu_ilp32
cargo build --target aarch64_be-unknown-linux-gnu_ilp32
```

Finally, we are developing a rich set of internal Rust libraries in Rust
built around an actor-based concurrency paradigm. This simplifies
asynchronuous programming by leveraging Rust language features such as
`async`, `await`, etc.

With respect to community engagement, Huawei has been leading the effort in
China, hosting the first Chinese Rust Conference during December 26-27 in
Shenzhen.  We have started to lead the community by carrying out a number of
activities, including creating Rust tutorials and Rust coding conventions in
Chinese for a vast number of developers who are interested in Rust. 

All these factors have led to increased adoption of Rust withing Huawei
and a smooth migration from C/C++ programs, which are dominant in the
telecom industry. As the leading company in this industry and a
founding member of the Rust Foundation, Huawei is committed to the
success of Rust and will continue contributing back to the Rust
community.

## C to Rust transpilation

To illustrate, one can take a close look at the following C program,
implementing the `100 doors' algorithm taken from Rosetta Code.

```c
#include <stdio.h>
 
int main()
{
  char is_open[100] = { 0 };
  int pass, door;
 
  /* do the 100 passes */
  for (pass = 0; pass < 100; ++pass)
    for (door = pass; door < 100; door += pass+1)
      is_open[door] = !is_open[door];
 
  /* output the result */
  for (door = 0; door < 100; ++door)
    printf("door #%d is %s.\n", door+1, (is_open[door]? "open" : "closed"));
 
  return 0;
}
```

The [c2rust](https://github.com/immunant/c2rust) transpiler initially
produces the following Rust code:

```rust
#![allow(dead_code, mutable_transmutes, non_camel_case_types, non_snake_case,
         non_upper_case_globals, unused_assignments, unused_mut)]
#![register_tool(c2rust)]
#![feature(main, register_tool)]
extern "C" {
    #[no_mangle]
    fn printf(_: *const libc::c_char, _: ...) -> libc::c_int;
}
unsafe fn main_0() -> libc::c_int {
    let mut is_open: [libc::c_char; 100] =
        [0 as libc::c_int as libc::c_char, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
         0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
         0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
         0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
         0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0];
    let mut pass: libc::c_int = 0;
    let mut door: libc::c_int = 0;
    /* do the 100 passes */
    pass = 0 as libc::c_int;
    while pass < 100 as libc::c_int {
        door = pass;
        while door < 100 as libc::c_int {
            is_open[door as usize] =
                (is_open[door as usize] == 0) as libc::c_int as libc::c_char;
            door += pass + 1 as libc::c_int
        }
        pass += 1
    }
    /* output the result */
    door = 0 as libc::c_int;
    while door < 100 as libc::c_int {
        printf(b"door #%d is %s.\n\x00" as *const u8 as *const libc::c_char,
               door + 1 as libc::c_int,
               if is_open[door as usize] as libc::c_int != 0 {
                   b"open\x00" as *const u8 as *const libc::c_char
               } else { b"closed\x00" as *const u8 as *const libc::c_char });
        door += 1
    }
    return 0 as libc::c_int;
}
#[main]
pub fn main() { unsafe { ::std::process::exit(main_0() as i32) } }
```

Although it is compilable, the resulting code is unmaintanable and
places too much responsibility on programmers to ensure its safety because all
functions are marked as `unsafe`.  Although the `c2rust` transpiler
supports refactoring commands, it is rather ad hoc, requiring further
tweaking with extra help of experienced Rust programmers. 

To take advantage of the safety guarantees of the Rust language, we have
chosen to leverage [TXL](http://txl.ca), an efficient source-to-source
transformation tool. We have developed a robust Rust parser for TXL and
used to develop automated refactoring patterns with a guarantee of
correct semantics, which allows us to achieve much safer and more
maintainable Rust code, e.g., 

```rust
// #include <stdio.h>
fn main() {
    let mut is_open: [i8; 100] = [0; 100];
    for pass in 0..100 {
        let mut door = pass as usize;
        while door < 100 {
            is_open[door] = !is_open[door];
            door += pass + 1;
        }
    }
    for door in 0..100 {
        print!(
            "door #{} is {}.\n",
            door + 1,
            (if (is_open[door]) != 0 {
                "open"
            } else {
                "closed"
            })
        );
    }
}
```

As one can see, there are no more `unsafe` blocks and the code is fully
understandable by programmers.

## Adapting end-to-end Rust tooling for Huawei
There are many end-to-end tools out there in the Rust community and we have
started to benefit from the interactions with developers of these tools.

Here are just a few examples. 

### `tokei`
Because trustworthy programming typically involves migrating programming
languages, we have adopted [`tokei`](https://github.com/XAMPPRocky/tokei) as our code
complexity metric tool, which can recognise as many as 200 languages. For
example, the following statistics show how many lines of code various
programming languages have been developed in Google's Fucshia project: 

![](img/RustConChina2020-yu-v49.png)\

It is relatively easy to plot the proportion of C, C++, Rust code in the evolution of
Fucshia, as follows: 

![](img/RustConChina2020-yu-v410.png)\

To accommodate the needs to processing multiple programming languages
in our projects, we have made a [pull request to
`tokei`](https://github.com/XAMPPRocky/tokei/pull/678) to support batch
processing of recognized languages.

### `cargo-geiger`
To improve safety, we would like as much code as possible to be checked
by the Rust compiler. Fortunately,
[`cargo-geiger`](https://github.com/rust-secure-code/cargo-geiger) does almost
this by counting the statistics of `unsafe` items such as `fn`, `expr`,
`struct`, `impl`, `trait`, and their occurrences in various dependent crates:

![](img/RustConChina2020-yu-v411.png)\

However, the statistics do not reflect the ratio of safe items, hence not
showing how much has been achieved overall for Rust projects. Therefore, we
made a [pull request](https://github.com/rust-secure-code/cargo-geiger/pull/167) to 
`cargo-geiger` to report the checked safe ratios of Rust projects. After it was
accepted, this tool has been used regularly by our product teams on daily
basis. A report will look like the following, which has made it easier to tell 
which crates have not been fully checked by the Rust compiler:

![](img/RustConChina2020-yu-v412.png)\
![](img/RustConChina2020-yu-v413.png)\



## Research on Rust through Deep Code Learning

As code bases from the Rust open-source community evolve and grow, new
developers need to learn the best practices, including but not limited to the
language itself. Statistical machine learning methods from large amount of
source code, also known as [Big Code](https://arxiv.org/abs/1709.06182), have
been considered by software engineering research communities: similar to the
machine learning problems for image processing and natural language processing
where vast number of features requires deep neural networks (DNN) to extract,
big code may also be used to train a DNN to reflect on statistical patterns of
programs, which is called `Deep Code Learning'.

In this respect, Huawei is pushing the limits by improving the state-of-the-art
of `cross-language' deep code learning.

For example, initial deep code learning methods are trained and evaluated using
the benchmarks of 52,000 C/C++ programs of 104 algorithm classes collected from
the programming courses of Peking University. Traditionally, tree-based
convolution neural networks (TBCNN) could achieve 94\% accuracy in algorithm
classification for this
dataset [(AAAI'16)](https://github.com/bdqnghi/tbcnn.tensorflow). A recent
progress of the SOTA using abstract syntax trees at the statement level
[(ICSE'19)](https://github.com/zhangj111/astnn) achieved 98\% accuracy. Our
recent progress pushes the SOTA even higher to achieve 98.4\% accuracy
[(AAAI'21)](https://arxiv.org/abs/2009.09777) by an innovation on Tree-based
Capsule Networks.  

Earlier, we have used cross-language datasets to show that the learnt model of one
language is applicable to another programming language. For example, using the
Rosetta Code datasets from Github, we show it possible to obtain 86\% accuracy
for algorithm classification (Java to C)
[(SANER'19)](https://github.com/bdqnghi/bi-tbcnn), and cross-language API mapping
problems (Java to C#)
[(ESEC/FSE'19)](https://github.com/bdqnghi/SAR_API_mapping). These statistical
language models have found multiple applications to software engineering, in terms of
code classification, code search, code recommendation, code summary, method
name prodiction, and code clone detection
[(ICSE'21)](https://github.com/bdqnghi/infercode). 

To analyse Rust projects, we have made another pull request to the Rust parser
project [`tree-sitter`](https://github.com/tree-sitter/tree-sitter/pull/863)
and XML serialization crate
[`quick-xml`](https://github.com/tafia/quick-xml/pull/250), which allow us to
feed the abstract syntax trees of Rust programs to train a deep code learning
model. The preliminary results are quite promising, the detection algorithms in
Rust can reach an accuracy as high as 85.5\%. This number is still climbing
as we continue working on improving toolchains.

A prototype of such an IDE is shown as an extension to the Visual Studio Code，where programmers are assisted with the recommendation of a suitable algorithm and an explanation of the choice.
![](img/RustConChina2020-yu-v414.png)\

## Conclusion

In summary, the Huawei Trustworthy Open-Source Software Engineering Lab is working
hard to provide programmers an end-to-end IDE toolchain that intelligently assists 
in maximizing safety and performance. 

A journey towards the vision of Trusted Programming has just begun and we hope
to work collaboratively with the Rust community, and the upcoming Rust
Foundation, to lead a smooth revolution to the Telecom software industry.  

