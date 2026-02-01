+++
draft = false
date = 2021-01-25T22:09:40+01:00
updated = 2023-01-04T22:09:40+01:00
title = "`tmux` 101"
description = ""
slug = ""
authors = ["Filippo"]
tags = [
    "tmux"
]
categories = []
externalLink = ""
series = []
+++

<span class="firstcharacter">H</span>owdy folks!

Work in progress!

Create a new session:
```shell
tmux new -s blueprint
```
List sessions:
```shell
tmux list-sessions
```
Reattach to a specific session:
```shell
tmux attach-session -t blueprint
```
## Additional resources

- [tmux - a very simple beginner's guide](https://www.ocf.berkeley.edu/~ckuehl/tmux/)
- [A beginner's guide to tmux](https://www.redhat.com/en/blog/introduction-tmux-linux)