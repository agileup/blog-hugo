+++ 
draft = false
date = 2014-07-10T20:03:19+09:00
title = "OSX/Linux 터미널에서 클립보드 복사 & 붙여넣기"
slug = "" 
tags = ["osx", "linux", "clipboard", "copyandpaste", "pbcopy", "pbpaste"]
categories = []
layout = ""
+++

## OSX

클립보드 복사는 `pbcopy`, 붙여넣기는 `pbpaste`

이 둘을 터미널 기본 파이프라인과 잘 조합해서 사용

```bash
// 복사
$ cat ~/foo.csv | pbcopy

// 붙여넣기
$ pbpaste > ~/bar.csv
```

## Linux(Ubuntu, Debian)

기본 패키지 저장소에 포함된 `xclip` 또는 `xsel`을 설치 후 사용

```bash
// 1. 설치
$ sudo apt install xclip xsel

// 2. alias 설정
$ vi ~/.bashrc

alias pbcopy='xclip -selection clipboard'
alias pbpaste='xclip -selection clipboard -o'

또는

alias pbcopy='xsel --clipboard --input'
alias pbpaste='xsel --clipboard --output'

// 3. 적용
$ source ~/.bashrc
```

사용법은 OSX와 동일


## Reference

> https://apple.stackexchange.com/a/15322  
> https://www.ostechnix.com/how-to-use-pbcopy-and-pbpaste-commands-on-linux/
