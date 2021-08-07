# strapi로 만든 API 배포 후 서비스에서 사용해보기

- 프리온보딩으로 진행한 [자란다 assignment]의 과제를 위한 프로젝트 (원티드 + 위코드 + 임팩트캠퍼스)

프리온보딩 세번째 과제였던 자란다의 assignment 🙆‍♀️
> [🏄🏻 Assignment3 자란다](https://www.notion.so/Assignment-3-9fdda37ca68a4748a3e034d80e4533ef)

이번 과제는 이전과 다르게 양이 방대하기도 하며 애자일이라는 새로운 업무 프로세스를 적용한 과제여서 그런지
3일이었던 과제기한이 5일로 늘었다.

8팀에 속해있던 나는 기본적으로 8명이서 한팀을 이루는 다른팀과 다르게 중도 포기자가 있어 5명으로 팀이 구성되었다. 
팀전체가 함께 진행하게 되는 프로젝트이기에 팀내 소통과 역할분담이 이전 프로젝트 보다 더욱 중요하고 책임감을 갖게 한다 🦁

### 첫번째 미팅
팀원분들중 한분인 영후님께서 피그마에 대략적인 UI 구조도를 그려와서 수월하게 
역할을 나눌 수 있었으며 어떤식으로 구조를 짜야할 지 한눈에 파악하기 쉬웠다.
![image](https://user-images.githubusercontent.com/61695175/128587837-5696f9d2-6e56-4a86-9fc2-05183e1b3dfb.png)

프론트는 구조나 데이터 플로우는 이해하겠지만 API 는..?!
기존 업무에서 항상 제공되던 API 없이 프론트엔드끼리만 로그인 회원가입, 기본적인 CRUD 를 만들기 위해서 백엔드를 대신할 무언가를 찾는게 우선이라 생각했다.

그러던 중 우연히 유튜브에서 들어본적 있던 [strapi] 오픈소스가 떠올랐고 제안했다. 
> [이전 포스팅 참고 🐥 ](/사용해보기/strapi.md)

사실 강의를 들은지 몇달이 되었고,, 한번 따라 해봤던 수준이라, 이를 활용해 우리의 프로젝트에 적용이 가능할지 확실하게 장담 할 순 없었지만..
테스트 해보기로 결정! 😅

이때 까지만 해도 프론트엔드가 모여있는 팀에 주어진 과제이기 때문에 과제를 내주신 분들의 의도가 맞는지 살짝 의아하긴했지만 더미데이터로 구성하여 과제를 완성하기보단 기한내 오픈소스를 활용해 api 쉽게 뽑을 수 있다면 이것도 괜찮은 방법이라 생각했다 🔥🔥

프로젝트를 시작하기전 우선 api를 배포하여 사용할 수 있는지에 대한 여부를 검색해봤다!

![image](https://user-images.githubusercontent.com/61695175/128588071-12b49969-e984-401b-b1dd-0bd3529ab546.png)

Heroku?? 다행히 이전 배포해본 경험이 있던 낯익은 사이트가 보였고 이를 활용해 보기로 결정
strapi 다큐먼트가 리액트 사이트 만큼이나 너무 잘 되어있어 하나씩 차근차근 따라해보기 시작 

백엔드 지식이 아예 없는 ㅠㅠ; 개발을 자바스크립트와 리액트로 시작한 1년경력의 코린이었기에 만약 api가 잘 나오지 않으면 어떡할지에 대한 불안함이 있었지만..
strapi는 그런 코린이들을 위한 오픈소스 이므로.. 무작정 따라해 보기로 한다. 😎😎

![image](https://user-images.githubusercontent.com/61695175/128588167-8bf436bf-0156-45bc-a4b5-c4458493f6da.png)

### strapi 프로젝트 생성
시작은 CRA와 비슷한 방식! strapi 에서 제공하는 CSP 'npx create-strapi-app my-project --quickstart'로 빠르게 프로젝트 생성!

사실.. 커스터마이징이 필요없는 api 라면 이게 끝..😅
이래도 되나 할 정도로 프로젝트 생성은 너무나 간단했고, 프로젝트 생성 후 'localhost:1337/admin'(default) 
에서 필요한 테이블이나 관계 설정 권한까지 프로젝트에 자동으로 생성 되는 시스템!

### heroku 배포 세팅

커스터마이징을 하기전 우리 프로젝트에 사용 될 수 있는지 테스트 해 보기위해 기본설정을 가진 strapi를 배포 해보기로 했다.
strapi 다큐먼트에 자세한 설명이 나와있어 하나씩 단계를 밟아보았다.

Heroku는 기본적으로 git 과 연동되어 배포하는 형식임으로 깃에 레파지토리를 연동시켜 커밋 🏋🏻‍♂️

```
cd my-project
git init
git add .
git commit -m "Initial Commit"
```

커밋 완료 후 내 프로젝트에서 heroku를 생성하자!
```
path: ./my-project/
heroku create
```
여기서 ```custom-project-name.heroku.com```로 URL를 커스터마이징 해 줄 수 있지만 (저는 그냥 홈페이지에서 바꾸는게 편하더라고요 😅)

### heroku + postgreSQL DATABASE 연동

이제부턴 기존 프로젝트 배포엔 없던 DATABASE Set-up 을 해줘야 한다! (갑자기 심장이 두근되기 시작한ㄷ..ㅏ)

위에서 언급한것과 같이 SQL,, DATABASE 등 나에겐 아직 너무 생소한 용어들이다 😹

영어는 너무 어렵지만 차근차근 해석해가며 읽어보기 시작했다.

```
Below you will find database options when working with Heroku. Please choose the correct database
 (e.g. PostgreSQL, MongoDB, etc.) and follow those instructions.
```

아래에서 heroku와 함께 작동하는 DB를 찾을 것이고...괄호에 있는것같은 올바른 DB를 골라서 지시를 따라라..!
맞나요!?🥲🥲

바로 아래 명세서를 보니 PostgresSQL을 세팅하는 방법이 나와있다.. 나는 암묵적으로 DB로 Postgres를 사용하는 것에 동의를 하게 된다. 


#### 1. Install the Heroku Postgres addon (opens new window)for using Postgres. <br/>
> 첫번째 스텝 Postgres addon 를 install 해라!


바로아래 shell명령어가 나와있으니 .. 오타방지를 위해 복붙해준다.

```Path: ./my-project/```
```
heroku addons:create heroku-postgresql:hobby-dev
```

![image](https://user-images.githubusercontent.com/61695175/128590404-b02cd970-f11f-44c4-974f-d4335aba84f0.png)
postgres addon를 세팅해주면 위와같이 heroku에 자동 연동된다


#### 2. Retrieve database credentials  <br/>
> 스텝 투, 데이터베이스 자격 증명 검색 (feat.google)


```heroku config``` 명령어로 나의 앱에 자격이 있는지(?)자동으로 증명해주는 듯 보인다..

만약 위 자격증명이 끝났나면 
``` DATABASE_URL: postgres://ebitxebvixeeqd:dc59b16dedb3a1eef84d4999sb4baf@ec2-50-37-231-192.compute-2.amazonaws.com: 5432/d516fp1u21ph7b.```
같은 형태의 DATABASE_URL이 뜰것이고 이는 배포 데이터베이스가 연동되었다는 뜻을 의미한다

![image](https://user-images.githubusercontent.com/61695175/128588715-edcf0116-daaf-4293-85ef-16fc7f747913.png)


#### 3. Set Database variables automatically  <br/>
> 세번째 스텝 데이터베이스 변수 자동 설정!


때때로 heroku에서 URL을 변경하므로 Heroku의 DATABASE_URL 환경 변수를 자동으로 업데이트해주는 설정이 필요하다
이는 간단하게 패키지만 설치해주면 된다.
```
npm install pg-connection-string --save
```


#### 4 Create your Heroku database config file for production  <br/>
> 네번째 스텝 production을 위한 데이터베이스 구성 파일 생성해주기!


폴더 생성 후 제공된 database.js 만 넣어주면 됩니다.
```path: ./config/env/production/database.js```

![image](https://user-images.githubusercontent.com/61695175/128588893-3c9a3c4a-2715-49eb-84c3-eae5e74b18ae.png)
파일 세팅이 완료된 후 이 데이터베이스가 구성파일이 될 수 있도록 NODE_ENV를 세팅해 주면 됩니다.

```
heroku config:set NODE_ENV=production
```

![image](https://user-images.githubusercontent.com/61695175/128588929-6d34802c-ef56-4425-a32c-12cb7704dd9f.png)

생각보다 일이 순조롭게 진행되는군 😍


#### 5 Create your Strapi server config for production <br/>
> 프로덕션을 위한 strapi 서버 구성 생성! (거의 다 왔습니다..!!)


이제부터 할 일은 Heroku의 도메인을 strapi에 알리기 위한 과정!
간단하게 ./config/server.js 에 아래와 같이 등록해줍니다. 
(MY_HEROKU_URL 에 프로젝트 배포주소 넣어주기)

```
module.exports = ({ env }) => ({
  url: env('MY_HEROKU_URL'),
});
```

![image](https://user-images.githubusercontent.com/61695175/128589060-f2c85674-63c1-40b5-a184-f16cb8568d52.png)

```
heroku config:set MY_HEROKU_URL=$(heroku info -s | grep web_url | cut -d= -f2)
```
그리고 .NET용으로도 Heroku 환경변수 설정이 필요합니다. (MY_HEROKU_URL = 프로젝트 배포 주소) <br/>
(여기서 .NET은 런타임에 애플리케이션 동작을 구성할 수 있는 다음과 같은 메커니즘을 제공합니다.)


#### 6 Install the pg node module <br/>
마지막으로 pg install 해주기

postgreSQL을 처음 사용해본 나게에 당연히 있을리 없는 pg node module 을 Install 해줌으로써 데이터베이스 연동 세팅이 끝나보이는듯 하다.

### 배포해보자!
git으로 heroku에 푸시하기

```
git push heroku HEAD:main
heroku open //배포가 완료되면 start 명령어
```

그렇게 열린 나의 (정식) 첫 strapi admin 사이트

![image](https://user-images.githubusercontent.com/61695175/128589203-cce3d46e-42bf-4da9-b655-9f64b0e165f7.png)

어드민 계정 세팅 후 들어가보자.

![image](https://user-images.githubusercontent.com/61695175/128589410-287a6f88-5900-4136-8a5e-a90d002066f5.png)

여기서 콘텐츠타입이나 관계설정등 백엔드 경험이 있었던 준영님의 도움으로 우리 프로젝트에 알맞는 테이블 과 타입들을 설정 할 수 있었다. <br/>
자란다 과제에서 필요한 Menu속성과 users 속성

![image](https://user-images.githubusercontent.com/61695175/128589467-0d2ca3da-f19b-476f-b2a7-da0917ebddec.png)

테이블 필드에는 우리과제에서 필요하지 않았던 기본설정들이 되어있긴 했지만 따로 삭제가 되지 않는 부분도 있었다.<br/> 
그래도 우리가 필요한 필드에 대해선 추가, 수정이 가능 하므로 추가해준다.
(card_info, address, age, is_admin ...)

![image](https://user-images.githubusercontent.com/61695175/128589511-2bfbcb9f-c1c6-4a88-9c44-eebae5f366f6.png)
메뉴도 설정해주고!

가장 중요한 관계설정! User도 여러가지의 메뉴를 가질 수 있고 메뉴도 여러명의 User 정보를 가질 수 있으므로 다대다 관계로 설정 완료! 

![image](https://user-images.githubusercontent.com/61695175/128589457-4fc026e0-b592-49cf-8f8f-698fbc2bd58a.png)

이렇게만 설정해준다면 strapi 기본설정 로그인과, 회원가입, 데이터를 GET 할 수 있는 기본 api설정은 완성이다!

<img src = "https://user-images.githubusercontent.com/61695175/128589579-b2778cda-b3c1-43e3-a246-1a04bf2f5309.png" width="300px"><img src = "https://user-images.githubusercontent.com/61695175/128589591-de9d34c0-7705-49ba-9184-70fa8beeead7.png" width="300px"><img src = "https://user-images.githubusercontent.com/61695175/128589620-af66b32b-dd6f-4f0f-9038-4863cf205a1b.png" width="300px">

로그인 같은 경우 strapi자체에 jwt토큰 까지도 다 설정 되어있어 따로 작업할 필요 없었다 👍👍 


## 🚧 주의사항

![image](https://user-images.githubusercontent.com/61695175/128589752-a7c0af24-8e58-4f69-aa07-5f604cb4f8e1.png) <br/>

**jwt 토큰 기한이 30일인데 리프레시 토큰을 제공하지 않는다는 이슈가 있다고 하니 실제 프로덕트에서는 사용하기엔 무리가 있지 않나 싶긴 하다 🥲**


하지만 마지막 남은 작업이 하나 있다
우리 프로젝트에 필요한 api중 하나인 회원정보수정!!(메뉴 허용여부 설정 변경 api)

많이 어려운 부분은 아니지만 블로그 양이 너무 방대해 짐으로.. 2부로 나누어 작성할 예정이다 ✨
