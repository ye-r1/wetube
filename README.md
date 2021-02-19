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

<br />

## # 3.0 MongoDB and Mongoose
M1 맥북에서 Homebrew를 설치하고 mongoDB 설치하는 방법
<br />
✅ /usr/sbin/softwareupdate --install-rosetta --agree-to-license
<br />
✅ arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
<br />
✅ arch -x86_64 brew install mongodb-community@4.4 <br /><br />
🔗 출처 : stackoverflow <br />
https://stackoverflow.com/questions/64963370/error-cannot-install-in-homebrew-on-arm-processor-in-intel-default-prefix-usr <br />
<br /><br />
⚠️ 다음 mongo로 실행한 후 에러가 뜨게되면 서버를 실행시켜준다.<br />
brew services start mongodb-community<br />
⚠️ DB 종료 <br />
exit<br />

MongoDB는 Database이고 Mongoose는 Database와 연결하게 해주는 것이다.
MongoDB는 NoSQL Database이고 규칙이 적고 유연해서 많은 부분을 수정할 수 있다
같은 서버에서 다양한 종류의 Database들을 사용할 수 있다.

<br />

## # 3.1 Connecting to MongoDB <br />
mongoose.connect()<br />
어디에 database가 저장되어있는지 알려준다<br />

``` javascript
mongoose.connect("mongodb://localhost:27017/we-tube”, {
    useNewUrlParser: true,
    useFindAndModify: false
});
```
``` javascript 
localhost:27017(포트번호) / we-tube(데이터베이스이름), {
    configuration 설정
}
```

`const db = mongoose.connection;`
<br />
DB연결

``` javascript
db.once("open", handleOpen);
db.on("error", handleError);
```
once는 한번 실행한다.<br />
db가 처음 오픈될때 실행할 함수, 에러발생시 실행될 함수이다.
<br />
init.js에 `import "./db”;` 를 추가해 db를 사용한다.

<br />

## # 3.2 Configuring Dot Env <br />
**dotenv** <br />
dotenv를 사용하면 원하는 내용을 변수로 만들어 숨길 수 있다.<br />
반드시 gitignore에 `.env`가 포함됐는지 확인해야한다.
<br /><br />
**저장된 변수를 사용할때**<br />
db.js
``` javascript
import dotenv from “dotenv”;
dotenv.config();
```
dotenv.config 를 써주면 `process.env.변수` 로 저장한 env 변수를 가져올 수 있다.

<br />

## # 3.3 Video Model <br />
DB를 생성하려면 우선 스키마를 작성해주어야한다.

model/video.js
``` javascript
import mongoose from "mongoose";

const VideoSchema = new mongoose.Schema({
    title: {
        type: String,
        required: "Tilte is required"
    },
});
```
사용할 항목의 타입을 작성하고, 필수로 필요한 항목이라면 required 를 쓴 후 에러메세지를 쓴다.

``` javascript
description: String,
```

상세 정의할 항목이 없다면 단순히 타입만 지정해주어도 좋다.

``` javascript
views: {
    type: Number,
    default: 0
},
```
항목의 기본값을 정해줄 수도 있다.

``` javascript
createdAt: {
    type: Date,
    default: Date.now
},
```

날짜를 넣어줄 수도 있다.<br />
현재 날짜를 반환하는 function을 써서 기본값을 반환한다.

``` javascript
const model = mongoose.model("Video", VideoSchema);
export default model;
```
video라는 이름의 모델을 만들고 비디오 스키마를 대입해준다.

``` javascript
import "./models/Video";
```
그리고 실제로 사용하려면 `init.js`에 import 해주어야한다.

<br />

## # 3.4 Comment Model<br />
서로 다른 데이터가 문맥상 연관성을 지니고 있을 때,
서로의 ref를 통해 연결 시켜준다.

models/video.js
``` javascript
comments: [
    {
        type: mongoose.Schema.Types.ObjectId,
        ref: "Comment"
    }
]
 ```

**mongoose.Schema.Types.ObjectId**<br />
mongoDB에 정의된 데이터타입 중 하나이고 객체를 구분하기 위해 사용된다.<br />
4바이트의 타임스탬프, 5바이트의 랜덤값, 3바이트의 랜덤에서 순차적으로 증가하는 값으로 이루어 진다.<br /><br />

video에 해당하는 모든 comment id가 담긴 [] 배열을 추가한다.<br />
다만, 데이터를 통으로 연결 시켜주는 것이 아닌, id(=데이터의 이름)만 넘겨주는 방식이다.<br /><br />
어느 model에서 참조해온건지 ref로 적어준다.<br />

<br />

## # 3.5 Home Controller Finished<br />

``` javascript
import Video from “../models/video”;

export const home = async (req, res) => {
    try {
        const videos = await Video.find({});
        res.render("home", { pageTitle: "Home", videos });
    } catch (error) {
        console.log(error);
        res.render("home", { pageTitle: "Home", videos: [] });
    }
};
```

`Video.find({});` <br />
Database에 있는 모든 video를 가져온다.<br />
<br />
async await<br />
실행 기다리게 하는 것, 성공적으로 끝나야하는게 아닌 그냥 끝날때까지 기다릴뿐 에러가 생겨도 다음블록을 실행한다.<br />
<br />
에러를 잡기 위해 try catch를 사용해서 에러를 잡는다.<br />

<br />

## # 3.6 Uploading and Creating a Video<br />
`<input type="file">`에 `accept="video/*”` 를 추가하면 비디오인 파일만 업로드 할 수 있다.<br />
<br />
file을 업로드하고 조작하려면 url을 반환하는 middleware인 multer가 있어야한다.<br/>
`<form enctype="multipart/form-data>`<br />
 그리고 form 태에 enctype을 추가하는 이유는 file을 보내기 때문에 폼의 인코딩이 달라야한다.<br />
<br /><br />
**multer로 middleware 만드는법**<br />
<br />
middlewares.js<br />
`const multerVideo = multer({ dest: "uploads/videos/" });`
destination으로 전달할 경로를 적는다.

`export const uploadVideo = multerVideo.single("videoFile");`<br/>
export 할 때 single은 하나의 파일만 upload할 수 있다, file의 url을 반환한다.
<br /><br />
single함수 안에 들어가는 videoFile은 `<input type=“file”>` 태그의 name 값이다.
<br /><br />
이제 파일을 업로드하면 서버에 있는 folder`(uploads/videos/)`에 Upload 된다.
그리고 postUpload라는 함수는 해당 file에 url 방식으로 접근한다.
<br />
multer가 자동적으로 이름은 임의로 바꾸고 확장자를 없애서 만든 file이 들어간다.
<br /><br />
그리고 video Controller.js에서 구조분해하여 file의 path를 가지고 온다.

``` javascript
const newVideo = await Video.create({
    fileUrl: path,
    title,
    description
});
res.redirect(routes.videoDetail(newVideo.id));
```

async await으로 나누어서 데이터를 기다리고 Video 스키마와 같은 항목인 fileUrl과 title, description을 담아 DB를 만들어준다.
<br /><br />
그 후에 videoDetail 페이지에 대입해준다.<br />
<br />

## # 3.7 Uploading and Creating a Video part Two<br />

use we-tube < DB 이름 > <br />
`show collections` 사용하고 있는 모델 (컬렉션)이 나온다.<br />
<br />
`db.videos.remove({})`<br />
db.<DB 이름> 지우기
<br /><br />
express 서버는 모든 주소에 route 경로 설정을 해야하기 때문에
upload 할때의 route도 미리 설정해주어야한다.<br />
<br />

app.js<br />
`app.use(“/uploads”, express.static(“uploads”));`<br /><br />
누군가 uploads 경로를 사용할때, express.static은 디렉토리에서 file을 보내주는 미들웨어이다.<br />
주어진 route에서 file만 전달해주는 역할이다, 따라서 이 경우엔 controller나 view를 확인하지 않는다.
file만 확인한다.<br />
<br />
이렇게 설정하게되면 /uploads로 갔을때 upload라는 디렉토리 안으로 들어가게 된다.
<br /><br />
video를 다운받아서 import 시킨것이다.

