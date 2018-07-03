+++ 
draft = false
date = 2014-05-28T18:10:35+09:00
title = "[Wordpress] Doesn't work WPTouch plugin after activate cache plugin"
slug = "" 
tags = ["wordpress", "plugin", "cache"]
categories = []
+++

얼마전 관리하던 사이트가 포탈 메인 노출 등으로 갑자기 동접이 폭증해서 서버가 죽어버리는 바람에 애를 꽤나 먹었던 기억이 있다.  
그렇다고 이런 간헐적인 상황때문에 서버 스펙을 올리는건 전반적으로 오버 스펙이 되기 때문에 다른 효과적인 방법을 찾아보았다.  
엄청난 해법이 있는건 아니고, 다소 번거로운 설정과 운영 이슈 때문에 기피했던 캐싱 설정을 맘먹고 적용했다!

> [Wordpress High Traffic Solutions](http://codex.wordpress.org/High_Traffic_Tips_For_WordPress)

워드프레스 캐싱 플러그인 양대 산맥인 **WP Super Cache**와 **W3 Total Cache** 중에서 좀 더 디테일한 설정이 가능한 **W3 Total Cache**를 설치했다.

1. 플러그인 활성화 후 세부 설정에서 Page cache, Minify, Browser cache, DB cache 등 각각 알맞게 체크 후 저장
2. 서버쪽에서 APC를 enable 하고, 기존의 apache prefork 설정에서 각각의 값들을 조금씩 올린 후 서버 재시작
3. Empty all cache!

구글/야후 사이트 성능 측정기로 돌려봤더니 역시 확연히 빨라진건 당연하고, 간단한 ab test도 비교적 무난하게 버티는것 같았다.  
그리고 사이트 특성상 모바일 유입이 반 이상이기 때문에 체감 속도가 얼마나 올라갔을지 확인하려고 사이트를 접속했는데..

가독성을 위해 적용해놓은 WPTouch 플러그인이 말을 듣지않고 실제 적용된 테마의 모바일 responsive 화면이 딱!  
당황하지 않고 두 플러그인 충돌 관련해 구글링을 해보니,

> [W3 Total Cache and WPTouch: Cooperating at last!](http://bit.ly/1rfLDHZ)

내용은 캐싱 설정에서 모바일 접근에 대한 User-agent 예외 목록을 설정해줘야 캐싱된 페이지가 아닌 WPTouch 뷰로 연결된다는 것.  
근데 방법만 알려주고 실제 예외 목록을 찾을 수가 없어서 조금더 키워드를 추가해 구글링을 해보니,

> [Optimizing Caching Plugins for Mobile Use](http://bit.ly/1rfM9G1)

좀 더 친절하게 각 플러그인에 맞춰서 설정 방법을 알려준다.

별다른 이슈 없이 그대로 설정한 뒤 다시 캐시를 비우고 데스크탑과 모바일 각각 접속해보니 바라던대로 알맞게 잘 보인다.  
구글링 전에 문제 원인을 떠올리지 못한게 좀 아쉽긴 하지만, 그래도 새로운 팁을 하나 더 알게된 것에 만족하면서 포스팅을 마친다.
