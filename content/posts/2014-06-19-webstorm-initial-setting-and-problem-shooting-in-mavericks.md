+++ 
draft = false
date = 2014-06-19T18:28:40+09:00
title = "[WebStorm] Initial setting and problem shooting in Mavericks"
slug = "" 
tags = ["webstorm", "setting", "mavericks"]
categories = []
+++

새로 시작하는 프로젝트 환경이 [MEAN](http://mean.io/) 기반에 협업 이슈도 있어서 코드 컨벤션도 맞출겸 WebStorm IDE 를 세팅했습니다.

유료 IDE라서 일단 Trial version 으로 접해보기 위해서 공식 홈페이지에서 다운로드를 받고 실행을 했는데 어떤 에러 메세지도 없이 아무 반응이 없었습니다.

근래에 Java 8 버전을 테스트하면서 버전 업그레이드를 한 후에 eclipse 및 aptana studio, titanium studio 등 자바 기반 모든 ide가 에러를 뿜으면서 실행이 제대로 안되서 고생했던 기억이 있기때문에 웹스톰 역시 같은 문제일것이라 가정하고 해결 방법을 찾아보았습니다.

```
At the moment all our products require Apple JDK 1.6 to be installed in order to run on Mac.
JDK 1.7 from Oracle is not officially supported yet and has known problems that stop us from using it by default.
Oracle JDK 1.7.0_40 has added support for Retina and works much better than previous versions on Mac.
You are welcome to give it a try in case you have any problems with Apple JDK.
To force running under JDK 1.7 edit /Applications/<Product>.app/Contents/Info.plist file, change JVMVersion from 1.6* to 1.7* :

<key>JVMVersion</key>
<string>1.7*</string>

See this answer for the known problems with JDK 1.7.
IDEA_JDK environment variable can be used to override the selected JDK,
you may need to run the product from the Terminal so that it sees your environment variables (Mac OS limitation):

open -a /Applications/<Product>.app/ .

Application About dialog will show the actual JDK version.
```

Reference

> https://intellij-support.jetbrains.com/entries/23455956-Selecting-the-JDK-version-the-IDE-will-run-under
