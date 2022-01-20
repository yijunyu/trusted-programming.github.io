---
layout: post
title: Contributions to the docs.rs project by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [docs.rs project](https://github.com/rust-lang/docs.rs).

### Add gitlab support

This [pull request](https://github.com/rust-lang/docs.rs/pull/1249) adds the support for gitlab information retrieval (for example, the number of stars or forks of a repository) and also create the architecture to greatly improve and simplify the adds of other platforms.

### Add footer to provide easier access to some information

We needed this [pull request](https://github.com/rust-lang/docs.rs/pull/1367) when we were about to add a link to the privacy policy page: only issue is that the top navbar on docs.rs was already quite "full". So instead, we decided to create a footer to reduce the load on the top navbar and also use it to add this new link.

### Fix navbar header overlay

This [pull request](https://github.com/rust-lang/docs.rs/pull/1462) fixes the invalid display of the top navbar when the window width is at some given values (in-between states).

### Fix invalid title on search results page

When you arrived on a search result pages, the title (you can see it on your browser tab) was "Releases - Docs.rs". This [pull request](https://github.com/rust-lang/docs.rs/pull/1458) fixes it.

### Move keyboard interactions handling out of the template inside a JS file

This [pull request](https://github.com/rust-lang/docs.rs/pull/1448) is mostly a cleanup to make code looks a bit better and centralized.

### Fix javascript errors

Some checks were missing in the javascript, creating errors visible in the web browser console. This [pull request](https://github.com/rust-lang/docs.rs/pull/1447) fixed it.

### Greatly improve docs.rs souce code viewer

This contribution is splitted in 3 pull requests:

 1. This [pull request](https://github.com/rust-lang/docs.rs/pull/1464) added a toggle mechanism on the source sidebar to allow to collapse it.
 2. This [pull request](https://github.com/rust-lang/docs.rs/pull/1477) made the source file sidebar scroll independent of the source file viewer scroll.
 3. And finally [this one](https://github.com/rust-lang/docs.rs/pull/1493) improved the global display of this feature.

### Unify keyboard events on docs.rs results

On <docs.rs>, you can navigate some pages using the keyboard. However, each page had its own handling for this behaviour. This [pull request](https://github.com/rust-lang/docs.rs/pull/1452) unifies the behaviour and the DOM.

### Update to new rustdoc style

Rustdoc changed how the sidebar is displayed, which makes the style much simpler overall. The problem on docs.rs is then not only to update its style, but to be able to handle both the old and new rustdoc styles without breaking one of the two. To do so, we detect the date on which the crate has been documented and set the correct style depending on it.

You can take a look at the pull request [here](https://github.com/rust-lang/docs.rs/pull/1579).

### Fix bug which prevented to click on the footer

Because of how the footer is displayed on docs.rs, we was going "under" the rustdoc content. To fix it, this [pull request](https://github.com/rust-lang/docs.rs/pull/1603) made it move on top.
