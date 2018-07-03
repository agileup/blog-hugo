+++ 
draft = false
date = 2014-02-27T21:44:55+09:00
title = "Laravel Overview"
slug = ""
tags = ["laravel", "php", "overview"]
categories = []
+++

* https://laravel.com/
* Taylor Otwell

---

### 특징

* 인증, 라우팅, 세션, 캐싱 등
* Composer, FrontController, MVC, IOC-DI, UnitTest

### 설치

* Composer 사용
* git clone

### 설정

* `app.php`, `database.php`

* VirtualHost 설정
> 프로젝트폴더/public

* app/storage 폴더 권한 777

### MVC

### Routing

* `app/route.php`
* method, filter, group 지원 - [문서](http://laravel-korea.org/docs/routing)

### Artisan CLI

* php artisan serve
* php artisan route
* php artisan controller:make [컨트롤러이름]

### Study 발표자료

* 정양파님 - Route [발표자료](http://slid.es/trauma2u/laravel-route)
* 윤종선님 - Form & View [발표자료](http://slid.es/xesper/input)
