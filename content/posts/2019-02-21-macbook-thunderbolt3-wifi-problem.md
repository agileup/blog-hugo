+++ 
draft = true
date = 2019-02-21T12:08:02+09:00
title = "맥북 신형 usb-c 허브 와이파이 간섭 문제 원인 및 해결방법"
slug = "macbook-thunderbolt3-wifi-problem" 
tags = ["macbook", "thunderbolt3", "wifi", "usb-c"]
categories = []
layout = ""
+++

<iframe src="https://www.google.com/maps/d/embed?mid=1QuZ9ZZiX0yRoc8cKsc2spKg79xtU3ev6" width="640" height="480"></iframe>

근래에 2018 맥북에어 신형을 잠시나마 사용해볼 기회가 있었는데, 사용중에 간헐적으로 잘 연결되어 있던 와이파이가 갑자기 끊긴 이후에 다시 연결되지 않아서 애를 먹었던 경험이 있어 해당 이슈에 대해 간략하게 기록해본다.

같은 증상으로 애플 상담받았었고 결론은 2.4ghz 충돌에 의한 와이파이 먹통이랍니다. 애플에서 만든 허브가 아니기에 그 제조사에서 이런 내용을 모르고 만든거라 생각이듭니다. 허브 제조사에 문의했지만 답변은 없더라고요

https://discussions.apple.com/thread/5564632
1. 케이블을 완전히 꽃지말고 살짝 1mm정도 빼면 된다는 의견이 있습니다.
2. 맥북프로 뒤쪽 경첩 부분에 하드드라이브나 usb디바이스를 놓으면 윗분 말대로 2.4GHz에 방해가 되지 놓지 말라네요. 5G는 문제가 없으실 듯 합니다.
" Do not place hard drives or other USB devices behind the rear of your Mac near at the hinge of your screen. The antennas for Wi-Fi and Bluetooth are located there"
도움이 되시길!

https://www.reddit.com/r/mac/comments/8hkeeu/macbook_pro_2017_wifi_issue_when_something/

https://www.clien.net/service/board/cm_mac/10729117
맥북 프로 터치바 USB 포트와 와이파이 간섭 문제 공유합니다.

USB 3.0(USB 3.1 Gen1) 대역폭과 2.4Ghz가 전파간섭이 생기는 문제로 USB 3.1 Gen2부터 해결되었다고 하나 아직 USB 3.1 Gen1을 사용하는 일부 3rd party 허브에서 여전히 발생하고 있는 증상입니다. 질문자님 맥 만의 문제가 아니며 모든 기기들의 문제라고 알고 있습니다.
5Ghz대역 Wi-Fi를 이용하시면 됩니다만 근본적으로 두 기기를 동시에 안 쓰는것 외엔 해결책이 없습니다 ㅠㅠ

현재 맥북 프로 터치바 15인치 사용중, USB-C 타입 허브를 연결하니 와이파이가 먹통이 되더군요, 그래서 집 와이파이 공유기 설정 페이지(tp-link는 
http://192.168.0.1/)로
 가서 무선설정 모드를 `11n 전용모드`로 변경 후 공유기 재부팅하니 잘되더군요

## 참고

- Mac에서 USB 기기 사용하기 https://support.apple.com/ko-kr/HT201163  
- USB 3.0* Radio Frequency Interference on 2.4 GHz Devices https://www.intel.com/content/www/us/en/io/universal-serial-bus/usb3-frequency-interference-paper.html
- https://namu.wiki/w/USB/%EB%B2%84%EC%A0%84#s-3.1
USB 3.0과 2.4 GHz 대역의 간섭 이슈가 있다.#[7] 2.4 GHz 대역은 무선 랜과 블루투스 같은 무선 장비가 많이 분포하는 주파수인데, USB 3.0 사용 시에 2.4 GHz 대역을 이용하는 기기가 먹통이 되면 바로 이 케이스에 걸린 것이다. 기기 제조사들 측도 인지하나 둘 가운데에 하나를 사용하지 않는 것 말고는 딱히 해결책이 없는 상태. 실제로 USB 3.0 규격 외장 하드 디스크와 2.4 GHz Wi-Fi를 이용하는 크롬캐스트를 같은 방에서 이용한 결과, 크롬캐스트 기능에 딜레이나 끊기는 현상이 일어나며, USB 3.0 규격 USB 메모리와 2.4 GHz 대역 주파수를 사용하는 무선 마우스를 서로 바로 옆 포트에 연결하면 마우스가 파킨슨병에 걸린 것처럼 덜덜덜 떨리면서 움직인다. 멀티밴드 와이파이를 지원하지 않는 기기를 사용하는데 간섭 현상이 일어나면 USB 선을 잠시 뽑아주자.
