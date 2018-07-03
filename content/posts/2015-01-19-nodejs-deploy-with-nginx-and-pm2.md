+++ 
draft = false
date = 2015-01-19T00:11:36+09:00
title = "[NodeJS] deploy with Nginx and PM2"
slug = "" 
tags = ["nodejs", "nginx", "pm2"]
categories = []
layout = ""
+++

Tips

PM2 자체 버전업(`npm update -g pm2`)을 한 뒤 pm2로 등록한 모든 프로세스를 재시작할 경우 정확한 상황은 아직 판단이 안되지만 간혹 기존 프로세스가 죽지 않고 계속 살아서 결과적으로 동일한 프로세스가 2개 이상 포크되어 원하지 않는 동작을 유발할 수 있다. 따라서 업데이트 후에는 반드시 `pm2 updatePM2` 명령으로 직접 현재 메모리에 올라가 있는 pm2를 업데이트를 해주면 해결된다.

Reference

> https://doesnotscale.com/deploying-node-js-with-pm2-and-nginx/
