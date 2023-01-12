---
layout: post
title: Rust_CodeBERT
toc: true
---
# Rust_BERT extension to support CodeBERT

```
Xiao Hang and Yijun Yu
Trusted Programming
Trustworthiness Software Engineering & Open Source Lab
Huawei Technologies, Inc.
```

CodeBERT is a transformer (BERT) based neural network framework pretrained on large amount of source code by Microsoft.
It is developed on top of Python (PyTorch). As a rewrite of the inference engine, Rust_BERT could speed up the inferencing
time for BERT-like models. However, it doesn't yet support CodeBERT.

In this feature, we developed an adaptation of CodeBERT model to extend it on Rust_BERT, which achieves 3x speedup. 

## Updates

[x] Proof-of-concept implementation for unsafe Rust code classification task
[ ] Test the model on more SE tasks orginally defined by CodeBERT
[ ] Release it as a library
