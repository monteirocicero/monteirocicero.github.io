---
layout: post
title: "How do I kill a specific process on listen?"
date: 2021-03-25 14:10:00 -0000
categories: Linux
---

This command shows how you can kill a process that is listening at a specific port
```
$ lsof -i :8080 -sTCP:LISTEN  |awk 'NR > 1 {print $2}'  |xargs kill -9
```

source: by https://serverfault.com/questions/847096/getting-pid-from-lsof-list
