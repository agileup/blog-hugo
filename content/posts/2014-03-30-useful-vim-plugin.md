+++ 
draft = false
date = 2014-03-30T16:45:29+09:00
title = "Useful vim plugin"
slug = "" 
tags = ["vim", "plugin"]
categories = []
+++


> PUG 한상헌님 소개로 알게된 각종 vim 플러그인을 실제로 설치하고 사용해보면서 정리한 문서입니다.  
> 환경: OS X Mavericks, iTerm2, homebrew

---

vim에 각종 플러그인을 설치함으로써 개발 편의성과 생산성을 높일 수 있습니다.
물론 VisualStudio, XCode, Eclipse 등 각종 IDE를 완전히 대체하기엔 무리가 있겠지만,
그럼에도 불구하고 여러 플러그인 설정을 통해 vim에서도 생산성을 끌어올릴 수 있습니다.  
  
플러그인을 설치하고 적용하는 방법은 크게 2가지가 있습니다.

1. pathogen
2. vundle


### Indent-Guides

* 인덴트(스페이스, 탭) 부분을 알기 쉽게 알맞은 색으로 하이라이팅 합니다.
* 설치 코드 `Bundle 'Indent-Guides’`
* 기본 키보드맵은 `\ig` 로 enable/disable 할 수 있습니다.
* 옵션을 통해 보다 상세한 설정이 가능합니다:

```bash
set ts=4 sw=4 et
let g:indent_guides_start_level = 2
let g:indent_guides_guide_size = 1
let g:indent_guides_enable_on_vim_startup = 0
```


### NERDTree

* 현재 디렉토리 및 상/하위 디렉토리와 파일들을 트리 형태로 조회하고 읽을 수 있습니다.
* 설치 코드 `Bundle 'The-NERD-tree’`


### surround

* quote를 double-quotes로, <p>태그를 <span> 태그로 빠르게 수정할 수 있는 플러그인
* 설치 코드 `Bundle ‘surround.vim'`


### matchit

* 괄호, 태그 등의 짝으로 편하게 이동할 수 있는 플러그인
* 설치 코드 `Bundle ‘matchit.zip’`
  
  
### powerline

* http://saulic.info/blog/vim-powerline-mac-osx-howto/
* https://kldp.org/node/125263


## Bundle install

I don't use a POSIX Shell (i.e. Bash/Sh)

For example, you use fish and errors result when running BundleInstall!

Vim will throw an error when running BundleInstall! if the default shell is not POSIX-compliant. Even if you manually switch to sh or bash from a different shell, the errors will continue if vim is not explicitly told to use sh or bash. The best way to rectify this is to:

Add set shell=bash to your .vimrc.  
Set the SHELL environment variable to sh or bash before running BundleInstall!.  
  
If using the fish shell, initial Vundle installation as well as updates can be performed by creating the following function at `~/.config/fish/functions/updatevim.fish` and then running updatevim to install/update Vundle and its bundles:

```bash
function updatevim
    set SHELL (which sh)
    vim +BundleInstall! +BundleClean +qall
    set SHELL (which fish)
end
```


### 아직 정리 못한 플러그인

- [x] Bundle 'gmarik/vundle’
- [x] Bundle 'Solarized’
- [ ] Bundle 'minibufexpl.vim'
- [ ] Bundle 'snipMate'
- [ ] Bundle 'taglist.vim'
- [ ] Bundle 'joonty/vdebug.git'
- [ ] Bundle 'ZenCoding.vim'
- [ ] Bundle 'SQLComplete.vim'
- [ ] Bundle 'vcscommand.vim'
- [ ] Bundle 'dbext.vim'
- [ ] Bundle 'netrw.vim'
- [ ] Bundle 'neocomplcache'
- [ ] Bundle 'vim-json-bundle'
- [ ] Bundle 'Syntastic'
- [ ] Bundle 'ctrlp.vim'
- [ ] Bundle 'Lokaltog/powerline', {'rtp': 'powerline/bindings/vim/'}


Plugins for PHP

- [ ] Bundle 'php.vim'
- [ ] Bundle 'checksyntax'
- [ ] Bundle 'shawncplus/phpcomplete.vim’
