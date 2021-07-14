# 리덕스의 원리와 불변성 ⚖️

## 리덕스 기본 용어 정리
> global state = A single source of truth <br />
> Actions = state is read-only <br />
> Reducers = Changes are made with pure functions

1. Action & action creators
2. Dispatch
3. Reducers
4. Store (state 와 reducers 을 포함 하는 것)

![Untitled](https://user-images.githubusercontent.com/61695175/125471256-869c1b29-d8b5-4ce9-8dad-95c80d06e23f.png)

리덕스 flow를 예를 설명하면 아래와 같다.
* **Order 주문 (action) ⇒ Restaurant server 레스토랑 서버 (dispatch) ⇒ chef 요리사 (reducer)**

```javascript
const action = {
//action의 이름을 type 에 정의합니다.
	type: "INCREMENT"
}
```

```javascript
//함수 정의
function increment(amount){
	return {
		type: "INCREMENT",
		payload: amount
	}
}

function decrement(){
	return {
		type: "DECREMENT"
	}
}

console.log(increment()) // {type : "INCREMENT"}
console.log(decrement()) // {type : "DECREMENT"}
```


```javascript
// 리듀서
function reducer(state = {count: 0}, action){
	// 액션타입에 맞춰 변경된 state 를 리턴합니다
	switch(action.type) {
        case "INCREMENT":
            return {
                count: state.count + action.payload
            }
        case "DECREMENT":
            return {
                count: state.count - 1
            }
				default:
						return state
    }
}

const store = redux.createStore(reducer)
console.log(store)
// {dispatch: dispatch(action), subscribe: subscribe(listener), getState: getState(), replaceReducer: replaceReducer(nextReducer)}

store.subscribe(()=>{
	console.log(store.getState())  // {count: 1}
})

// dispatch로 액션값 혹은 함수값을 가져와 리턴 할 수 있습니다.
store.dispatch({type: "INCREMENT"}) 
store.dispatch(increment(5)) // {count: 6}
store.dispatch({type: "INCREMENT"}) // {count: 2}
store.dispatch(decrement())
store.dispatch({type: "WEIRD"})
```

## 리덕스 사가
### 용어정리

- **fetchData**: REQUEST_LIKE 액션을 처리하는 제너레이터 함수이며, 이를 사가 함수라고 함
- while 문을 사용하여 무한 반복하도록 함
- **take**: 인수로 전달된 액션 타입을 기다림, 여러 개의 액션을 기다릴 수도 있음REQUEST_LIKE 액션이 발생하면 다음 줄의 코드가 실행되며,yield take는 액션 객체 반환
- **put**: 새로운 액션을 발생시킴결과적으로 store.dispatch 메서드를 호출하는 효과가 있음
- **call**: 입력된 함수를 대신 호출함입력된 함수가 프로미스를 반환하면 프로미스가 처리됨 상태가 될 때까지 기다림
- **watcher**: 여러 개의 사가 함수를 모아 놓은 함수이며, 사가 미들웨어에 입력
- **all, fork**: 사가 함수를 추가할 때 사용하는 함수로 사가 함수를 추가할 때는 아래와 같이 작성

## 리덕스 사가 컨셉트! 😛
Concept
Effect는 미들웨어에 의해 수행되는 명령을 담고있는 평범한 자바스크립트 객제라고 생각하면 된다.
saga는 Effect를 yield(생산)하고, Middleware는 Effect를 처리한다.

## 리덕스 사가 generator
```javascript
function* gen() {
	console.log("a");
	console.log("b");
}

// *(generator)이 선언되었기 때문에 next()를 이용해 호출 할 수 있다.
const g = gen()
//undefined

g
> gen{<suspended>}

g.next()
a
b
> {value: undefined, done: true}
```

```javascript
function* gen(i){
	yield i;
	yield i+10;
}
const g = gen(5)
const gObj = g.next()

gObj
{value: 5, done:false}

const jObj = g.next()
jObj 
{value: 15, done: false}
g.next()
{value: undefined, done:true}
```

```javascript

function* gen(i){
	yield i;
	yield i+10;
	return 25;
}
const g = gen(5)
g.next()
{value: 5, done:false}
g.next()
{value: 15, done:false}
g.next()
{value: 25, done:true}
```

## 리덕스 툴킷?
action typed을 정의하고, action creator를 만들어 redux-saga를 사용하는 경우 saga를 만들고
reducer까지 만들어아 하는 반면, 리덕스 툴킷을 사용하면 createSlice를 이용해 한 번에 가능하다.

### 사용예시 
```javascript
//타입선언
interface User {
  uid: string;
  displayName: string;
  photoURL: string;
}

interface UserState {
  user: User;
}

// state 값 초기화
const initialState: UserState = {
  user: {
    loading: false,
    data: null,
    error: null,
  }
}

const slice = createSlice({
  name: 'user',
  initialState,
  // 리듀서 정의
  reducers: {
    signInRequest(state, action: Action) {
      state.user = {
        loading: true,
        data: null,
        error: null,
      };
    },
    signInSuccess(state, { payload: userInfo }: PayloadAction<User>) {
      state.user = {
        loading: false,
        data: userInfo,
        error: null,
      };
    },
    signInFailure(state, { payload: error }: PayloadAction<Error>) {
      state.user = {
        loading: false,
        data: null,
        error,
      };
    },
  },
})    
```




