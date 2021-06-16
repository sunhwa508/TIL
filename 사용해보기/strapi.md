# strapi
백엔드 없이 백엔드 지식 없이 API를 만들어 보자!

코드를 한줄도 안쓰고 RestApi를 만들 수 있는 라이브러리 📚📚

[strapi 사이트](https://strapi.io/documentation/developer-docs/latest/getting-started/quick-start.html#_1-install-strapi-and-create-a-new-project)

```
yarn create strapi-app my-project --quickstart
```

```
yarn develop
```
으로 서버를 구동시킬수있습니다~

## 기본 화면 구성과 항목 추가하기
![image](https://user-images.githubusercontent.com/61695175/122241289-66b33380-cefd-11eb-9769-107975bfc2d8.png)
> strapi 다운로드 후 로그인 브라우저 창이 뜰 것이다 이것이 바로 대시보드!
> 우선 대시보드에서 Create New collection Type을 이용해 크게 필드를 생성해줍니다.



![image](https://user-images.githubusercontent.com/61695175/122244243-b1ce4600-ceff-11eb-8d59-1fdf4b172034.png)

> collection Type을 생성했다면 네비에서 타입들을 확인 할수있고 각 필드의 항목을 추가할 수도 있습니다! ✨✨

![image](https://user-images.githubusercontent.com/61695175/122244405-d3c7c880-ceff-11eb-8268-5659e9eb6a0b.png)

> 테스터용 유저도 하나 생성해 줍니다~


![image](https://user-images.githubusercontent.com/61695175/122244532-ec37e300-ceff-11eb-8360-5159d560928c.png)

> 이후 포스트맨으로 테스트 해봅니다~
> url를 잘 적어두고 Send를 보내면 땋
> 잘 나오는걸 확인 할 수 있습니다~~


## 로그인하기 (JWT토큰이 자동생성?! 👸👸)
Strapi는 기본적으로 로그인까지 전부 세팅이 되어있습니다

![image](https://user-images.githubusercontent.com/61695175/122245218-8009af00-cf00-11eb-996e-43f2e8afd001.png)

> 대시보드에서 미리 등록해둔 user을 통해 로그인하게되면 jwt토큰이 자동 생성되어있는것을 확인 하실 수 있습니다.!


이외에 커스터 마이징을 위해선 Strapi 문서를 참고하여 수정 가능합니다.



