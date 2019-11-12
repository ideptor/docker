# 가장 빨리 만나는 도커 - 이재홍지음 / 

## CH08 Docker로 Application 배포하기

### 8.1 서버 한대에 애플리케이션 배포하기

#### 8.1.1 개발자 PC 에서 git 설치 및 저장소 생성하기

#### 8.1.2 개발자 PC 에서 Node.js로 웹 서버 작성하기

```js
var express = require('express')
var app = express();

app.get(['/', '/index.html'], function(req, res) {
	res.send("Hello Docker");
});

app.listen(80);
```
