# strapi로 api 만들고 커스텀하기!

#### [strapi 커스텀 하기 전 기본설정](https://velog.io/@sunhwa508/strapi%EB%A1%9C-%EB%A7%8C%EB%93%A0-API-%EB%B0%B0%ED%8F%AC-%ED%9B%84-%EC%84%9C%EB%B9%84%EC%8A%A4%EC%97%90%EC%84%9C-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0)

## Users 정보 수정하는 api
지금부터 strapi를 살짝 변형해 users의 정보를 update 하는 api를 만들어볼것이다.<br />
어떻게? 👇🏻

![화면 기록 2021-08-07 오후 7 57 13](https://user-images.githubusercontent.com/61695175/128597947-771a925d-f922-42f4-a870-0ac6bbf76088.gif)

구글링과 strapi 깃허브를 참고하여 user 상태를 업데이트 할 수 있는 예제들을 쉽게(?) 찾을 수 있었다.

다큐먼트를 정독하며 함수와 변수를 공부하기엔 무척이나 부족한 시간을..탓으로 돌리며
예제를 보며 이해하고 적용해보기로 했다.

👀

[도움이 됐던 stack overflow](https://stackoverflow.com/questions/65973564/change-user-password-in-strapi) <br />
[strapi git](https://github.com/strapi/strapi/blob/master/packages/strapi-plugin-users-permissions/controllers/user/admin.js) 


커스텀할 api의 폴더를 만들어보자 이전 블로그에서 설명했던것 처럼 create-strapi-app을 사용하면 기본적으로 세팅이 되는 폴더가 있다.<br />
그 중 extensions/users-permissions 에 커스텀파일을 추가해 작성 할 예정이다.

<image src="https://user-images.githubusercontent.com/61695175/128598028-cf0ccbbc-f012-461b-8274-b07a3a1eed6e.png" width="200px"/>


## 폴더구조
1. route.js 를 세팅해준다
2. controllers 폴더에 api가 해줄 역할을 작성한다.

```
// strapi 공식문서 참조
method (string): Method or array of methods to hit the route (e.g. GET, POST, PUT, HEAD, DELETE, PATCH).
path (string): URL starting with / (e.g. /restaurants).
handler (string): Action to execute when the route is hit following this syntax <Controller>.<action>.
config/policies (array): Array of policy names or paths (see more)
```

```path: /extensions/users-permissions/config/routes.json```

```javascript
{
    "routes":[
        {
            "method": "PUT",
            // Update를 해주는 api 를 만들어야 하므로 PUT 사용!
            "path": "/custom/:id",
            // custom에 들어갈 문구가 ${BASE_URL}/custom/:id 여기들어갈 주소 정보가 될 것이다~!
            // "path": "/restaurants/:category/:id", 이런식의 세팅 많이 보던 구조다..!
            "handler": "User.update",
            "config": {
              "policies": [],
              "prefix": ""
            }
            // 환경설정 부분은 특이점이 없는 관계로 기본형으로 둔다.
    }]
}
```

이렇게 라우터 세팅을 마치고 본격적으로 controller를 세팅해준다.

```path: /extensions/users-permissions/controllers/User.js```

```javascript

module.exports = {
  /**
   * Update a/an user record.
   * @return {Object}
   */
  
   async updateUser(ctx) {
    const advancedConfigs = await strapi
      .store({
        environment: '',
        type: 'plugin',
        name: 'users-permissions',
        key: 'advanced',
      })
      .get();

    const {
      params: { id },
      request: { body },
      state: { userAbility, admin },
    } = ctx;
    
    // strapi admin 을 통해 세팅해 준 field 값들을 여기서 가져와 수정할 수 있다.
    const { email, username, password, menus, card_info, age, address } = body;

    const { pm, entity: user } = await findEntityAndCheckPermissions(
      userAbility,
      ACTIONS.edit,
      userModel,
      id
    );

```

**에러처리**
```javascript

    if (_.has(body, 'menus') && !menus) {
      return ctx.badRequest('menus.notNull');
    }
    
  if (_.has(body, 'menus')) {
      // strapi 메소드를 이용해 users, users-permissions 쿼리에 있는 menus 를찾는다
      const userWithSameMenus = await strapi
        .query('user', 'users-permissions')
        .findOne({ menus });
        
      // 쿼리가 없거나, 중복되었을 경우 Error를 던진다.
      if (userWithSameMenus && userWithSameMenus.id != id) {
        return ctx.badRequest(
          null,
          formatError({
            id: 'Auth.form.error.menus.taken',
            message: 'menus.alreadyTaken.',
            field: ['menus'],
          })
        );
      }
    }
    
````

```javascript
  // 마지막 단계에서 body에 새로 세팅된 값을 적용 시켜 준다.
  const sanitizedData = pm.pickPermittedFieldsOf(body, { subject: pm.toSubject(user) });
  const updateData = _.omit({ ...sanitizedData, updated_by: admin.id }, 'created_by');
    
  const data = await strapi.plugins['users-permissions'].services.user.edit({ id }, updateData);

  ctx.body = pm.sanitize(data, { action: ACTIONS.read });
```

같은 방식으로, menus 대신 username, id 등 변경하고 싶은 필드만 바꿔 세팅해주면 끝 👏
그래도 자바스크립트로 작성되어 있기 때문에 완벽하진 않겠지만 과제를 위해 사용할 수 있는 api를 완성 할 수 있어 뿌듯하다 😹



# Referance
[strapi 공식문서](https://strapi.io/documentation/developer-docs/latest/development/backend-customization.html#routing)
