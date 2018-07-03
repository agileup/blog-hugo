+++ 
draft = false
date = 2015-01-03T23:31:57+09:00
title = "[PUSH NOTIFICATION] Tips for APNS & GCM"
slug = "" 
tags = ["push", "notification", "apns", "gcm"]
categories = []
+++

## MESSAGE SIZE

- APN이 허용하는 최대 PAYLOAD 크기는 256 BYTES(http://goo.gl/vYsOJq) 라서 DEVICE TOKEN 과, 부가 정보 등 JSON의 KEY 값을 제외하면 실제 메시지 길이는 그렇게 여유 있지 않음.
- 서버에서 꼭 필요한 데이터를 제외한 잔여 크기 만큼 계산해 보여줄 메시지(ALERT)를 잘라내야 함.
- GCM은 4096 BYTES 까지 허용하기 때문에 푸시로 보낼 데이터의 내용을 감안 했을때 거의 제한이 없다고 봐도 됨.

## ERROR HANDLING

#### APN

- TRANSMISSION ERROR를 전송 결과로 받을 수 있음. ERROR CODE와 함께 푸시 보낸 정보도 함께 들어오는데 여기서 코드가 8번이 "INVALID TOKEN"에 해당하니 해당 토큰은 저장소에서 삭제해도 무방.
- 또한 FEEDBACK(http://goo.gl/WORVjY) 서비스를 지원하여 앱이 지워졌거나 기타 이유로 푸시가 기기에 도달되지 못했을 경우 APN 서버가 이를 기억해서 피드백을 등록한 써드파티 서버로 알려줌. 근데 여기서 중요한 점이 실제로 유효한 피드백을 받으려면 해당 기기에 APN 서버와 통신하는 앱이 하나라도 있어야 함. 보통 일반적인 환경에선 걱정할 필요가 없지만 개발 중인 테스트 앱 환경에서는 SANDBOX 서버를 사용하기 때문에 단일 앱으로는 푸시 피드백을 테스트할 수 없음.

> [Sending Notification Requests to APNs](https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/sending_notification_requests_to_apns)

#### GCM

