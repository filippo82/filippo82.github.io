+++
draft = false
date = 2021-01-25T22:09:40+01:00
updated = 2023-01-04T22:09:40+01:00
title = "How to build your personal website with Hugo"
description = ""
slug = ""
authors = ["Filippo"]
tags = [
    "hugo"
]
categories = []
externalLink = ""
series = []
+++

<span class="firstcharacter">H</span>owdy folks!

Work in progress!

## `hugo.toml`

Available `pygmentsStyle` styles: https://xyproto.github.io/splash/docs/all.html
See this comment from the author of `hugo-code` theme: https://github.com/luizdepra/hugo-coder/issues/603

## Create a draft for a new article

When you feel creative and want to start writing a new blog post,
you can create a draft by executing

```shell
hugo new posts/my-first-post.md
```

The new draft will be added in the `/contents/posts` directory.
The `draft` value for the new draft will be initially set to `true`.
Once the draft is ready and can be published, the `draft` value will need to be set to `false`.

## Spruce it up

I like using info and warning boxes but they are not available out-of-the-box with Hugo.
For this reason, I installed [hugo-notice](https://github.com/martignoni/hugo-notice),
a Hugo theme component which provides a shortcode to display nice notices.
It also supports dark mode! It provides four notice types: warning, info, note and tip.

## Test and view locally

Hugo provides a development web server which allows you to easily view your website.
You can start the web server by executing

```shell
hugo server
```

and then you can navigate to [https://localhost:1313](https://localhost:1313) in a browser
to view your website.

## Additional resources

* [The complete guide to Hugo file structure and code organization](https://jpdroege.com/blog/hugo-file-organization/)
* [The Ultimate Guide to Hugo Sections](https://cloudcannon.com/blog/the-ultimate-guide-to-hugo-sections/)
