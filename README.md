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

<br />

## # 2.15 Partials with Pug<br />
layout 에서 `block content` 선언해준 후 페이지 컴포넌트에서 `extends`를 이용해 가져왔을때
children에 들어갈 내용을 작성할 수 있다.<br />
```javascript
extends layouts/main
    block content
        p Login
```
<br />

`#{console.log(" ")}` <br />
pug 안에서 자바스크립트를 쓸 수 있다<br />

<br />

## # 2.16 Local Variables in Pug<br />
locals 미들웨어<br />
global 변수로 사용하도록 해주는 것<br />
라우터들 보다 상위에 위치시켜야 모든 라우터에도 공통적용이 가능함<br />
next()를 통해 다음 함수로 넘겨줘야만 사용가능하다.<br />

middleware.js<br />

```javascript
const localsMiddleware = (req, res, next) => {
    res.locals.siteName = "WeTube";
    next();
}
```

`res.locals` 에 변수를 정의해주고<br />
`#{siteName}` 으로 템플릿 내에서 사용할 수 있다.<br />

<br />

## # 2.17 Template Variables in Pug<br />
```javascript
res.render("home”, {siteName : home});
```
<br />
여기서 render할때 첫번째 인자는 views 안에 있는 템플릿 파일을 가르킨다.<br />
두번째 인자는 해당 템플릿에 변수를 정의할 객체이다.<br />

<br />

## # 2.18 Search Controller<br />
```javascript
export const search = (req, res) => {
    const {
        query: { term: searchingBy }
    } = req;
    res.render("search", { pageTitle: "Search", searchingBy });
};
```

videoController.js<br />
search form에서 보낸 req로 쿼리값을 구조분해하여 받아온다. 그리고 변수로 search 에 값을 보내준다.<br />

<br />

## # 2.22 Home Controller part Two<br />
mixin<br />
pug의 함수, 자주 반복되어 재활용되는 코드를 묶어둘 수 있다. <br />


join의 get과, post 방식을 쪼개서 처리한다.<br />
bodyParser를 이용하면 post로 오는 데이터들을 `body`로 가져올 수 있다.

```javascript
const {
    body: { name, email, password, password2 }
} = req;
```
