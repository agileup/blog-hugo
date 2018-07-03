+++ 
draft = false
date = 2014-06-12T01:22:47+09:00
title = "[AngularJS] 기초 간단 정리"
slug = "" 
tags = ["angularjs"]
categories = ["dev"]
layout = ""
+++

### 동작 순서

1. 브라우저가 html을 로드 (DOM을 파싱한다.)
2. Angular.js를 로드한다
3. DOM Content Loaded Event를 기다린다.
4. DOM이 모두 로드되면 ng-app 지시자를 찾는다.
5. ng-app에서는 dependency injection 을 위해 사용되는 $injector를 생성한다.
6. injector 지시어는 어플리케이션의 모델을 위한 컨텍스트가 되는 루트 스코프를 생성한다.
7. 최종적으로 ng-app을 기준으로 하위DOM을 컴파일하고 rootScope와 링크시킨다.


### 기본 개념

1. Scope

 - Scope는 모델 변경을 감지하고 표현하기위한 책임을 갖는다
 - Scope는 DOM 구조와 가깝게 하이어라키 구조를 갖는다

2. Model

 - 모델은 화면 템플릿에 합쳐지는 데이터를 가지고 있는 일반 자바스크립트 객체이다. (데이터라고 생각하면 된다.)
 - Scope는 항상 모델을 참조하고 있다.

3. View

 - 템플릿 스트링과 모델을 합쳐서 HTML을 만들고 DOM으로 해석되어 Browser에 표현된다 .
 - Angular는 템플릿이 HTML이어서 바로 DOM으로 해석되고 DOM안에 directive가 템플릿 엔진인 $compile지시어를 통해 $watch를 설정하고 모델의 변경을 계속 감시하게 된다.
 - View는 템플릿으로 Scope의 투영체이고, Scope는 Model과 View의 연결하며 controller로 이벤트를 보내는 역할을 한다.

4. Controller

 - Controller는 View뒤에서 반드시 수행하는 코드이다.
 - Controller 역할은 모델을 생성하고 콜백 메소드를 가지고 View로 퍼블리싱을 담당한다 .
 - Controller 는 자바스크립트이고 업무적 행위를 정의한다. 또한 DOM rendering 정보가 일체 없다 .

5. Directives (지시어)

 - 지시어는 HTML 을 확장하여 주고 행위를 일으키는 주체이다 .
 - 예를들어 앞의 예제에서 보았듯이 데이터 바인딩을 위한 이중 중괄호 표기{{}}, 컨트롤러가 뷰의 어느 부분을 감독할지를 지정하는 ng-controller, 인풋을 해당 모델의 구성물에 바인딩하는 ng-model 모두 Directive를 이용한 확장 문법이다.


### Dependency Injection

* https://github.com/angular/angular.js/wiki/Understanding-Dependency-Injection


### Yeoman

* http://www.thinkster.io/angularjs/eqq96ECqkT/1-getting-your-project-set-up-with-yeoman
* http://yeoman.io/codelab/keep-going.html

### Unit Test

* http://andyshora.com/unit-testing-best-practices-angularjs.html

### MEANio

* http://mean.io/#!/docs


### with Bootstrap

* http://angular-ui.github.io/bootstrap/

### 참고

* http://blog.whydoifollow.com/post/angularjs-where-to-start
* http://www.nextree.co.kr/p3241/
