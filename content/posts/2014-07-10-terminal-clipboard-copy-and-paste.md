+++ 
draft = false
date = 2014-07-10T20:03:19+09:00
title = "터미널에서 클립보드 복사 & 붙여넣기"
slug = "" 
tags = ["osx", "linux", "clipboard", "copyandpaste", "pbcopy", "pbpaste"]
categories = []
layout = ""
+++

클립보드 복사는 `pbcopy`, 붙여넣기는 `pbpaste`. 이 둘을 리눅스 기본 파이프라인과 잘 조합해서 사용.

리눅스나 OSX 모두 터미널에서 동일하게 사용 가능.

```bash
// 복사
$ cat ~/foo.csv | pbcopy

// 붙여넣기
$ pbpaste > ~/bar.csv
```

Reference

> https://apple.stackexchange.com/a/15322
