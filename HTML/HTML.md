# HTML



## 목차

[div](#div)

### HTML 이란?

Hyper Text Markup Language - 프로그래밍 언어가 아님



Hyper Text - 참조를 통해 사용자가 한 문서에서 다른 문서로 즉시 접근할 수 있는 텍스트

- ex) http / html

Markup Language - 마크업 언어이기 때문에 단순하게 데이터를 표현하기만 한다



> 즉 웹 페이지를 작성하기 위한(구조를 잡기 위한) 언어
>
>  웹 컨텐츠의 '의미'와 '구조'를 정의



### 태그

p, a , b , strong 등 다양

br > 띄어쓰기 

내용이 없는 태그 - br, hr, img, input, link, meta

##### form

- action > 어디로 보낼지
- method > http method(get,post..)

##### input

- 입력이 들어가는 곳(type 따라 다름)
- 종류가 엄청나게 많음
- https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input

##### div

영향 x 그냥 구조를 잡기 위해 씀

##### 시맨틱 태그 > 잘 작성해야 검색을 했을 때 잘 나옴(검색엔진) > 역할 자체는 div와 같지만 그냥 표현을 위해 해주는것

###### 시맨틱 태그의 종류

- header - 문서 전체나 섹션의 헤더(머릿말 부분)
- nav - 내비게이션
- aside - 사이드에 위치한 공간, 메인 콘텐츠와 관련성 적은 콘텐츠
- section - 문서의 일반적인 구분, 컨텐츠의 그룹을 표현
- article - 문서,페이지,사이트 안에서 독립적으로 구분되는 여역
- footer - 문서 전체나 섹션의 푸터(마지막 부분)

###### 요약

- 개발자 및 사용자 뿐만 아니라 검색엔진 등에 의미 있는 정보 그룹 태그로 표현
- 단순히 구역을 나누는 것 뿐만 아니라 '의미'를 가지는 태그들을 활용하기 위한 노력
- Non 시멘틱 > div, span // h1,table도 시맨틱 태그로 볼수 있음
- 요소의 의미가 명확해지기 때문에 코드의 가독성, 유지보수 쉬워짐
- 검색엔진최적화(SEO)를 위해 메타태그, 시맨틱 태그활용 필요

### head, body

head > 브라우저 상단에 뜸 (브라우저 자체에 표시되진 않음)

Opne Graph Protocol > 헤드부분에 페이스북이 구현한 기술 og:title(메타태그)

body

- header - 큰 머리말
- section - 중간
- footer - 아래





### DOM(Document Object Model)

- 문서의 구조화된 표현(Structured Representation)을 제공하며, 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방버을 제공하여 그들이 문서 구조, 스타일 내용등 을 변경할 수 있도록 도움을 준다



#### 속성

<태그(a) 속성(href)="https://google.com"> </태그(/a)>

- id, class, hidden, lang, style, tabindex, title



