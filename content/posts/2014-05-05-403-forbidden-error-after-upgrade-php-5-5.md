+++ 
draft = false
date = 2014-05-05T17:47:40+09:00
title = "403 forbidden error after upgrade php 5.5"
slug = "" 
tags = ["php"]
categories = []
+++

개인적으로 운영하는 서버에 PHP 버전을 판올림한 후 느닷없이 모든 페이지에서 403 Forbidden 에러가 발생했습니다.

구글링을 해본 결과 RootDirectory 권한 문제라는 글이 많았는데, 이건 아무리봐도 해당 경우가 아닌것 같아서 다른 방법을 찾아보던 중

업데이트 기록을 보니 기존에 2.2 버전이였던 apache 데몬이 2.4로 판올림 된걸 확인할 수 있었습니다.

> http://httpd.apache.org/docs/2.4/upgrading.html  

아파치 문서를 찾아보니 **Access Control** 설정을 변경하도록 안내되어 있습니다.

```bash
Order allow,deny
Allow from all
```

2.2 버전에서 이렇게 설정된 부분을 아래와 같이 변경해주면 됩니다.
  
```bash
Require all granted
```

그 밖에 모듈 관련해서도 설정이 바뀌는 부분이 있는데 이는 크게 문제될만한 부분이 없어 그냥 한번 읽고 넘어가면 좋겠습니다.  

> 참고: http://stackoverflow.com/questions/18609087/getting-a-403-error-after-upgrading-to-php5-5  

