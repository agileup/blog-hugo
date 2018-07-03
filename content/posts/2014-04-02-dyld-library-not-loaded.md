+++ 
draft = false
date = 2014-04-02T17:15:30+09:00
title = "dyld: Library not loaded: /usr/local/lib/libpng15.15.dylib"
slug = "" 
tags = ["brew"]
categories = []
+++

brew로 이것저것 library를 관리하다 보면 어느순간 위와 비슷한 에러 메세지를 만날 경우가 있다.  

그럴때는 당황하지 않고,  

```bash
$ brew update
$ brew upgrade
```

그리고 현재 버전의 php 재설치

```bash
$ brew reinstall php55
```

끝
