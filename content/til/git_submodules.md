+++ 
draft = false
date = 2023-11-04T13:04:34+01:00
updated = 2023-11-04T13:04:34+01:00
title = "TIL - Git submodules"
description = "Quick recipes for working with git submodules"
slug = ""
authors = ["Filippo"]
tags = ["til"]
categories = ["til"]
externalLink = ""
series = ["til"]
+++

## List existing submodules

```shell
git submodule status
```

## Add a submodule

```shell
git submodule add --depth 1 git@github.com:filippo82/sample-apps.git
```

