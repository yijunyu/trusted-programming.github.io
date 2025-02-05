---
layout: post
title: Our Rust Mission at Huawei
toc: true
---


[中文](our-rust-mission-at-huawei_cn.html)

# Trusted Programming -- Our Rust Mission at Huawei

*Yijun Yu*

Chief Expert on Trusted Programming\
Trustworthy Open-Source Software Engineering Lab &\
Ireland Research Centre\
Huawei Technology, Inc.

*Amanieu d'Antras*

Principal Rust Expert\
Trustworthy Open-Source Software Engineering Lab &\
Ireland Research Centre\
Huawei Technology, Inc.

*Nghi D. Q. Bui*

Research Scientist\
Trustworthy Open-Source Software Engineering Lab &\
Ireland Research Centre\
Huawei Technology, Inc.

## Innovations by Rust

Since 2015, Rust has consistently been voted as the most loved
programming language in the StackOverflow survey.

![]({{site.baseurl}}/images/2021-02-07/RustConChina2020-yu-v42.png)

There has also been an increasing number of publications on Rust at the recent top
programming languages and software engineering conferences. 

![]({{site.baseurl}}/images/2021-02-07/RustConChina2020-yu-v43.png)

If that's not enough, a recent Nature 2020 article, `Why Scientists are Turning
to Rust', says that there is increasing momentum on the adoption of Rust
amongst scientists.

![]({{site.baseurl}}/images/2021-02-07/RustConChina2020-yu-v41.png)

## Initial adoption of Rust at Huawei 

At Huawei, we aim to engineer trustworthy software systems in the
world's largest telecom industry. 

For example, we are working to migrate parts of our codebase towards
Rust, which is safer and as performant as C/C++. To assist our
developers in this process, we are leveraging the open-source
[C2Rust](https://c2rust.com/) transpiler to generate Rust code directly
from C. We have created automated tools to refactor and clean up this
generated Rust code through source-to-source transformations.

We are also developing a rich set of internal libraries in Rust
built around an actor-based concurrency paradigm. This simplifies
asynchronous programming by leveraging Rust language features such as
`async`, `await`, etc.

All these factors have led to increased adoption of Rust withing Huawei
and smooth migration from C/C++ programs, which are dominant in the
telecom industry. As the leading company in this industry and a
founding member of the Rust Foundation, Huawei is committed to the
the success of Rust and will continue contributing back to the Rust
community.

## Contributions to Rust community from Huawei

We also contribute significant features back to the Rust community. For
example, our recent contributions to the Rust compiler enable the
compilation of Rust programs for big-endian and
[ILP32](https://developer.arm.com/documentation/dai0490/latest/)
variants of AArch64.  These changes enable Huawei and other hardware
companies to run Rust code on networking hardware which commonly uses these architecture variants.  This contribution is achieved with the
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

With respect to community engagement, Huawei has been leading the effort in
China, strategically sponsored [the first Rust China Conf](https://2020conf.rustcc.cn) during December 26-27 in
Shenzhen.  We have started to lead the community by carrying out several
activities, including creating Rust tutorials and Rust coding conventions in
Chinese for a vast number of developers who are interested in Rust. 

## Adapting end-to-end Rust tooling for Huawei

There are many end-to-end tools out there in the Rust community and we have
started to benefit from the interactions with developers of these tools.

Here are just a few examples. 

### `tokei`

Because trustworthy programming typically involves migrating programming
languages, we have adopted [`tokei`](https://github.com/XAMPPRocky/tokei) as our code
complexity metrics tool, which can recognize as many as 200 languages. For
For example, the following statistics show how many lines of code various
programming languages have been developed in Google's Fucshia project: 

![]({{site.baseurl}}/images/2021-02-07/RustConChina2020-yu-v49.png)

It is relatively easy to plot the proportion of C, C++, Rust code in the evolution of
Fucshia, as follows:

![]({{site.baseurl}}/images/2021-02-07/RustConChina2020-yu-v410.png)

To accommodate the needs to processing multiple programming languages
in our projects, we have made a [pull request to
`tokei`](https://github.com/XAMPPRocky/tokei/pull/678) to support batch
processing of recognized languages.

### `cargo-geiger`

To improve safety, we would like to know how much code has been checked by the Rust
compiler. Fortunately,
[`cargo-geiger`](https://github.com/rust-secure-code/cargo-geiger) does almost
this by counting the statistics of `unsafe` items such as `fn`, `expr`,
`struct`, `impl`, `trait`, and their occurrences in various dependent crates:

![]({{site.baseurl}}/images/2021-02-07/RustConChina2020-yu-v411.png)

However, the statistics do not reflect the ratio of safe items, hence not
showing how much has been achieved overall for Rust projects. Therefore, we
made a [pull request](https://github.com/rust-secure-code/cargo-geiger/pull/167) to 
`cargo-geiger` to report the checked safe ratios of Rust projects. After it was
accepted, this tool has been used regularly by our product teams on daily
basis. A report will look like the following, which has made it easier to tell 
which crates have not been fully checked by the Rust compiler:

![]({{site.baseurl}}/images/2021-02-07/RustConChina2020-yu-v412.png)
![]({{site.baseurl}}/images/2021-02-07/RustConChina2020-yu-v413.png)

## Research on Rust through Deep Code Learning

As codebases from the Rust open-source community evolve and grow, new
developers need to learn the best practices, including but not limited to the
language itself. Statistical machine learning methods from a large amount of
source code, also known as [Big Code](https://arxiv.org/abs/1709.06182), have
been considered by software engineering research communities: similar to the
machine-learning problems for image processing and natural language processing
where a vast number of features requires deep neural networks (DNN) to extract,
big code may also be used to train a DNN to reflect on statistical patterns of
programs, which is called `Deep Code Learning'.

In this respect, Huawei is pushing the limits by improving the state-of-the-art
of `cross-language' deep code learning, through a technical collaboration with
[The Open University, UK](https://mcs.open.ac.uk/yy66) and [Singapore
Management University](http://www.mysmu.edu/faculty/lxjiang/).

For example, initial deep code learning methods are trained and evaluated using
the benchmarks of 52,000 C/C++ programs of 104 algorithm classes collected from
the programming courses of Peking University. Traditionally, tree-based
convolution neural networks (TBCNN) could achieve 94% accuracy in algorithm
classification for this
dataset [(AAAI'16)](https://github.com/bdqnghi/tbcnn.tensorflow). A recent
progress of the SOTA using abstract syntax trees at the statement level
[(ICSE'19)](https://github.com/zhangj111/astnn) achieved 98% accuracy. Our
recent progress pushes the SOTA even higher to achieve 98.4% accuracy
[(AAAI'21)](https://arxiv.org/abs/2009.09777) by an innovation on Tree-based
Capsule Networks.  

Earlier, we have used cross-language datasets to show that the learned model of one language applies to another programming language. For example, using the
Rosetta Code datasets from Github, we show it possible to obtain 86% accuracy
for algorithm classification (Java to C)
[(SANER'19)](https://github.com/bdqnghi/bi-tbcnn), and cross-language API mapping
problems (Java to C#)
[(ESEC/FSE'19)](https://github.com/bdqnghi/SAR_API_mapping). These statistical
language models have found multiple applications to software engineering, in terms of
code classification, code search, code recommendation, code summary, method
name prediction, and code clone detection
[(ICSE'21)](https://github.com/bdqnghi/infercode). Such models also have the capability to
transfer the knowledge across many tasks, thus it will reduce the effort to retrain the models for 
each of the tasks separately.

To analyze Rust projects, we have made another pull request to the Rust parser
project [`tree-sitter`](https://github.com/tree-sitter/tree-sitter/pull/863)
and XML serialization crate
[`quick-xml`](https://github.com/tafia/quick-xml/pull/250), which allow us to
feed the abstract syntax trees of Rust programs to train a deep code learning
model. The preliminary results are quite promising, the detection algorithms in
Rust can reach an accuracy as high as 85.5\%. This number is still climbing
as we continue working on improving toolchains.

A prototype of such an IDE is shown as an extension to the Visual Studio
Code，where programmers are assisted with the recommendation of a suitable
algorithm and an explanation of the choice.

![]({{site.baseurl}}/images/2021-02-07/RustConChina2020-yu-v414.png)

## Conclusion

In summary, the Huawei Trustworthy Open-Source Software Engineering Lab is working
hard to provide programmers an end-to-end IDE toolchain that intelligently assists 
in maximizing safety and performance. 

A journey towards the vision of Trusted Programming has just begun and we hope
to work collaboratively with the Rust community, and the upcoming Rust
Foundation, to lead a smooth revolution to the Telecom software industry.  

# Updates
![]({{site.baseurl}}/images/2021-02-07/our-rust-mission-at-huawei.mp4)

- Here is a demo of our [CRustS transpiler](http://185.190.206.130)
