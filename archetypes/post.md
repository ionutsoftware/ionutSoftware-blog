---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
reply:
uri: "https://ionutSoftware.net/post/{{ .Name }}"
categories: ["note"] # note, reply, anything else
tags:
draft: true
---

