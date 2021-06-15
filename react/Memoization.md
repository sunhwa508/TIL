# Memoization

- Memoization는 본질적으로 캐싱이라 할 수 있습니다.
```
const cache = {}

function slow(a) {
  if (cache[a]) return cache[a]
  
  const result = /* Complex logic */
  cache[a] = result
  return result
}
```
캐시에 정보가 있다면 복잡한 함수를 실행하지 않고 캐시에서 정보를 가져다 사용 할 수 있습니다.

## 리액트 hooks 적용하기
## useMemo
```
const result = useMemo(() => {
  return slowFunction(a)
}, [a])
```
useMemo 첫 인수는 메모하려는 복잡한 계산을 수행하는 함수이며 두 번째 인수를 모든 종속성의 배열입니다.

## Referential Equality 참조 동등성
Referential Equality에 익숙하지 않은 경우 기본적으로 두 값의 참조가 동일한 지 여부를 정의합니다.

```
function Component({ param1, param2 }) {
  const params = { param1, param2, param3: 5 }

  useEffect(() => {
    callApi(params)
  }, [params])
}
```

```
function Component({ param1, param2 }) {
  const params = useMemo(() => {
    return { param1, param2, param3: 5 }
  }, [param1, param2])

  useEffect(() => {
    callApi(params)
  }, [params])
}
```
위 코드를 아래와 같이 변경 하는 경우 param1 과 param2가 변경되지 않았을 경우 캐시 된 값으로 설정됩니다.
종속성 배열에서 함수를 사용해야 하는 경우 useCallback을 사용할 수 도 있습니다.

## useCallback
```
const handleReset = useCallback(() => {
  return doSomething(a, b)
}, [a, b])
```
useMemo가 종속성 배열을 기반으로 값을 캐시한다면  useCallback은 값을 캐시하는 대신 함수를 캐시하는 데 사용됩니다.


## useMemo & useCallback의 차이점
useMemo있지만 주요 차이점은 useMemo종속성이 변경 될 때마다 전달 된 함수를 호출하고 해당 함수 호출의 값을 반환한다는 것입니다.
useMemo는 종속성이 변경될 때 마다 전달된 함수를 호출하고 해당 함수 호출의 값을 반환하는데 반해
useCallback은 전달 된 함수를 호출하지 않고 종속성이 변경 될 때마다 전달 된 함수의 새 버전을 반환합니다.

```
useCallback(() => {
  return a + b
}, [a, b])

useMemo(() => {
  return () => a + b
}, [a, b])
```
위와 같이 useCallback은 전달 된 함수를 반환하고, useMemo는 결과를 반환합니다.

## React.memo
React.memo함수 는 props가 변경되지 않는 한 React.PureComponent 래핑 된 컴포넌트 React.memo가 다시 렌더링 되지 않는다는 점에서 매우 유사합니다.
```
React.memo(function Component(props) {
  // Do something
})
```
 구성 요소를 래핑하더라도 구성 요소 React.memo의 내부 상태 또는 컨텍스트가 변경되면 다시 렌더링됩니다.
 
 ## 정리
 리액트는 메모를 처리하는 여러가지 방법이 내장되어있으며 이를 활용하면 
 따로 추가 (캐싱관련)코드를 작성하지 않고도 성능향상을 위한 코드를 작성 할 수 있습니다.
