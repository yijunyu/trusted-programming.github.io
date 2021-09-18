# Reflections on the Rust Conference 2021

Yijun Yu

```
Chief Expert in Trusted Programming
Director of Trustworthiness Lab
Ireland Research Centre
Huawei Technology, Inc.
```

The Rust conference ended successfully. Although it had to be held online due to the pandemic, over 2,000 people participanted the Discord live discussions at the conference, which is another testament to the popularity and importance of Rust programming language in software industry. In contrast, our developers had little interests in Apple's iPhone 13 launch event on the same day :-) Interestingly, the leading Rust experts spoke at the conference are from diverse backgrounds and are young and energetic.

The initial keynote addresses of the conference were given by Niko Matsakis and Mara Bos, presenting a vision of the development of Rust language and library, respectively. The following are some of the thoughts of Huawei experts who participated:

1. From the perspective of safe and trustworthy programming language, Niko emphasizes that although the performance of the Rust language is already close to that of the C language, the ease of learning and use of the Rust language needs to catch up with those of scripting languages. This is not to say that Rust should have all the features of various programming languages, rather, the emphasis is on addressing the pain points in practical uses. For example, it is not that hard to add the Async/Await language feature, but extremely difficult to constrain the added feature to introduce minimal changes to the language syntax. By doing that, we can make Rust's future brighter. Guillaume Gomez, a Huawei expert in the Rust community for years, also believes that Rust could do a better job with grammar and documentations which he is working on. Lily Mara's later presentation echoes this goal that: To better popularize Rust, it is desirable to simplify some of its features, even at the expense of performance where it is tolerable. These performance losses can easily be made up after more language features are mastered. As Linux Kernel is also trying to use Rust for some of its development, in the near future Rust could be more ubiquituous. As a major system vendor, therefore, Huawei is leading the development of the Rust open source community in China, focusing on the development of root technologies for trustworthy systems. It is consistent with the goals of the Rust community.
2. From the perspective of library development, Mara introduces an in-depth story: The Rust standard library already has mutex implementations based on OS-specific implementations (e.g. pthreads, Win32), but these APIs are designed for C use cases and don’t map well to Rust, which requires expensive workarounds such as boxing the mutex. Parking lot is a new implementation designed for Rust which significantly improves performance, made by Huawei expert Amanieu d'Antras in 2018. However its inclusion in the standard library has lead community discussions for years and has not been properly resolved. While both Rust and Parkinglot have been improved and developed over the years, they have never been able to combined. Under Mara's leadership, the Rust community has adopted a strategy of removing the obstacles over the last few months by making some  baby steps which may lead to a significant solution. For example, getting Microsoft to cooperate with the revision of their operating system API specification related to mutex. This has played a role in integrating the development of other operating systems. These steps helped rebuilding the confidence in the Rust community to integrate parkinglot. For open source development tasks, even as hard as Parking Lot integration, can learn from the lessons: with determination and leadership to gradually identify and remove obstacles, the momentum of Rust's Library development is even more promising. From this year onwards, the Rust Library team will reorganise into two specialized teams, one focusing on the maintenance of the Library APIs and the other on the development of the core Library itself. It is likely that we will see more library features, such as integrating parkinglot, SIMD, and inline assembly into the basic standard library of the Rust language 2021 Edition.


# Rust大会感想

Rust大会顺利闭幕了。虽然由于疫情影响，大会必须在线进行，但是空前地有多达2000人参与会议互动，
从另一方面证明Rust编程语言在软件工程业界的受欢迎和重视程度。
相比之下，码农们对于同一天的召开的Apple 十三香产品发布会没有什么感觉 :-) 
作为开发者中的翘楚，来自Rust社区与会演讲的专家背景各异，年轻活跃。

大会的主题发言由Niko Matsakis和Mara Bos给出，分别介绍Rust语言和Rust库发展的愿景。以下是华为参会专家的部分感想：

1. 从系统安全可信编程语言的视角看，Niko强调虽然Rust语言性能上已经接近C语言，易学易用方面还需要向脚本语言看齐。这不是说Rust要通吃所有编程语言特性的能力，而是要解决实际使用中的痛点。比如，增加Async/Await这个语言特性并不难，难的在于如何让这个增加的特性对语法引入最小的修改。做到这一点，我们才能让Rust的未来发展得更好。作为耕耘Rust社区多年的专家，Guillaume Gomez也认为，在语法和文档适配方面Rust可以做得更好。后面Lily Mara的演讲中，也回应了这个目标：为了更好地普及Rust，哪怕在不重要的地方牺牲一点性能，简化Rust的一些特性也是可取的。掌握了更多的语言特性以后，这些性能的损失很容易可以补回来。另外，Linux Kernel也在部分尝试使用Rust开发，因此，在不远的将来，每一个系统设备里面都有可能有Rust的身影存在。因此，作为系统大厂，华为在Rust方面引领中国开源社区的发展，主攻系统根技术的可信发展，这跟Rust社区的目标十分一致。

2. 从语言特性本身发展的视角看，Mara介绍了一个很有代表性的叙事：Rust标准库中已经基于特定操作系统（pthreads，win32）初步实现了mutex, 但是操作系统中的这些API是针对C的用例设计的，还不能直接映射到Rust的一般用例上。如果要在Rust上绕过这些困难实现mutex需要昂贵的boxing方式。Parking lot是华为专家Amanieu d'Antras在2018年针对Rust的场景实现的高性能mutex库。可是在标准库中引入parking lot在社区引起了经年的讨论，仍然无法彻底解决。虽然在这个过程中，Rust和Parking lot都分别得到了很好的改进和发展，但是始终无法如愿把两者结合。在Mara的领导下，这几个月Rust社区采取了化整为零的策略，逐一排除这个跨平台同步互斥特性的障碍，获得了重大进展：比如让微软配合修改了操作系统API文档规约，间接地起到了整合操作系统发展的作用，重新拾起了Rust社区整合parking lot的信心。对于开源建设，即使是Parking Lot这样的硬骨头，有了化整为零，逐步排查障碍的决心和领导力，Rust的Library库的发展势头更加不可阻挡了。今年以后，Rust Library团队会专业化分为两个团队，一个专注于Library API的维护，另一个专注于Library核心本身的发展，我们很有可能看到更多的库特性，比如把SIMD集成到Rust语言的基本标准库中来。
