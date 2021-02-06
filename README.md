WeTube
=============

Cloning Youtube with Vanilla and NodeJS

<br />

## # 2.4 Handling Routes with Express<br /><br />

GET = 단순히 페이지를 가져오는 것<br />
POST = 정보를 전달<br />
req = POST 로 전달한 정보를 요청해서 정보를 받음<br />
res = 정보를 응답<br />

<br />

## # 2.6 Express Core: Middlewares<br />

라우팅 후 콜백함수 사이에서 동작할 함수<br />
주의) 미들웨어에 next()를 덧붙여야 다음 액션이 실행된다, 그렇기에 미들웨어에서 다음 행동을 중단 시킬 수 있다.<br />
별도로 적용할때에는 routing, callback 사이에 직접 위치하며<br />
전체에 적용할 경우 app.use()를 사용하면 해당 코드 아래에 있는 모든 코드에 적용된다<br />

<br />

## # 2.7 Express Core Middlewares morgan, helmet, cookie-parser, body-parser<br />
Morgan = 실행 관련 로그를 남김<br />
helmet = 기초 보안<br />
cookieParser = 쿠키를 다룰 수 있음<br />
bodyParser = form 데이터를 서버로 받아와서 활용가능<br />

<br />

## # 2.9 MVC Pattern part One<br />
MVC = > Model, View, Control<br />
<br />
Model = data<br />
View = data가 어떻게 생겼는지<br />
Control = data를 보여주기 위한 함수<br />

<br />

## # 2.13 Installing Pug<br />
app.set() 애플리케이션의 설정을 할 수 있는 함수<br />
<br />
`app.set("view engine", "pug");`<br />
애플리케이션의 뷰 엔진을 퍼그로 바꾼다.<br />
<br />
view 파일들의 위치는 기본으로 /views인데<br />
바꾸고 싶으면 `app.set("views", "")`을 사용하여 경로 이름을 바꾸면 된다.<br />
<br />
pug<br />
템플릿 언어<br />
`<p> hello </p>`를 `p hello` 로 적으면 된다.<br />
<br />
컴파일시 pug가 일반 html 코드로 자동 변환된다<br />
<br />
이렇게 작성한 템플릿을 전달하기 위해 기존 send()를 사용하는 대신 render()를 사용한다.<br />

