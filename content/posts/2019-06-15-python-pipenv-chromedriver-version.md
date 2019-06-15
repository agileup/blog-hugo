+++ 
draft = false
date = 2019-06-15T16:20:51+07:00
title = "python selenium 개발 chromedriver 버전 문제 해결"
description = ""
slug = "python-pipenv-chromedriver-version" 
tags = ["python", "pipenv", "selenium", "chromedriver", "homebrew"]
categories = []
layout = ""
externalLink = ""
+++ 

python 프로젝트에서 selenium으로 특정 사이트 크롤링 작업이 필요했는데 pipenv로 환경설정을 마친 후에 바로 예상치못한 에러를 만났다.

```sh
selenium.common.exceptions.SessionNotCreatedException: Message: session not created: This version of ChromeDriver only supports Chrome version 75
```

에러메시지를 보면 설치된 크롬드라이버 버전과 내 os에 설치된 크롬 버전이 맞지 않는다는 내용인데,  
앞선 프로젝트에서 필요해 brew로 설치했던 chromedriver가 일괄 업데이트 되면서 버전업이 된게 문제의 원인인듯 했다.

현재 OS에 설치된 크롬 버전은 주소창에 `chrome://version`에서 확인해보면 `74`버전이고 해당 버전에 맞는 [크롬드라이버](http://chromedriver.chromium.org/downloads)는 `74.0.3729.6` 버전이다.

```sh
$ brew cask install chromedriver
```

위 명령어를 통해서 그냥 간편하게 설치할 경우 자동으로 최신 버전(`75.0.3770.90`)의 크롬드라이버가 설치된다.
설치된 크롬드라이버 정보는 아래 명령어를 통해 확인할 수 있다.

```sh
$ brew cask info chromedriver
```

해결을 위해선

1. 크롬 버전 업그레이드: 74 → 75
2. 크롬드라이버 버전 다운그레이드: 75 → 74

두가지 중 편한 방법을 선택하면 된다.

나는 두번째 방법으로 해결했는데, 해결 방법은 다음과 같다.  
`homebrew cask`를 이용해 설치한 모든 패키지의 다운그레이드는 동일한 방법으로 가능하다.

1. 기존 설치된 패키지 제거
2. [Homebrew Cask GitHub 저장소](https://github.com/Homebrew/homebrew-cask)에서 `Casks` 폴더 내 설치 필요한 패키지 검색
3. 필요 패키지 이름의 `*.rb` 파일 선택 후 해당 파일의 History 조회
4. 커밋 로그에 알맞은 버전 확인 후 해당 커밋 시점에 raw file link 복사
5. 특정 버전의 패키지 설치

```sh
# 기존 버전 삭제
$ brew cask uninstall chromedriver
==> Uninstalling Cask chromedriver
==> Unlinking Binary '/usr/local/bin/chromedriver'.
==> Purging files for version 75.0.3770.8 of Cask chromedriver

# 특정 버전 설치
$ brew cask install https://raw.githubusercontent.com/Homebrew/homebrew-cask/0d1e0888e1cc3365e96249d4f606eb293725f6b4/Casks/chromedriver.rb
==> Downloading https://raw.githubusercontent.com/Homebrew/homebrew-cask/0d1e0888e1cc3365e96249d4f606eb293725f6b4/Casks/chromedriver.rb.
######################################################################## 100.0%
==> Satisfying dependencies
==> Downloading https://chromedriver.storage.googleapis.com/74.0.3729.6/chromedriver_mac64.zip
######################################################################## 100.0%
==> Verifying SHA-256 checksum for Cask 'chromedriver'.
==> Installing Cask chromedriver
==> Linking Binary 'chromedriver' to '/usr/local/bin/chromedriver'.
🍺  chromedriver was successfully installed!

# 설치 버전 확인
$ brew cask info chromedriver
chromedriver: 75.0.3770.90
https://sites.google.com/a/chromium.org/chromedriver/home
/usr/local/Caskroom/chromedriver/74.0.3729.6 (14.1MB)
From: https://github.com/Homebrew/homebrew-cask/blob/master/Casks/chromedriver.rb
==> Name
ChromeDriver
==> Artifacts
chromedriver (Binary)
```

드라이버 버전을 낮추고 다시 python 프로젝트를 실행해보면 정상적으로 에러 없이 동작하는걸 확인할 수 있다.

> reference  
- http://chromedriver.chromium.org/downloads  
- https://github.com/Homebrew/homebrew-cask


