## Map타입 (javascript 의 object와 닮은형태)
```
void main(){
  Map dictionary = {
    'apple':'사과',
    'banana':'바나나',
    'watermelon':'수박'
}

print(dictionary) 
//  {
    'apple':'사과',
    'banana':'바나나',
    'watermelon':'수박'
}
print(dictionary['apple']) //사과
```

## Map다루기
```
void main(){
  Map dictionary2 = {};
  dictionary2.addAll({
    'apple':'사과',
    'banana':'바나나',
    'watermelon':'수박'
  });
}

dictionary2.remove('apple')
print(dictionary2) // {banana:바나나, watermelon:수박}

// 단 같은 값의 키가 여러개 존재 할 수 없다.👱‍♀️👱‍♀️
// 같은 키의 value를 추가할 경우 오버라이딩 된다.
dictionary2['banana']='프론트몽키'
print(dictionary2) // {banana:프론트몽키, watermelon:수박}
```

## List 와 Map 선언법
1. List list = new List();
2. Map dictionary = {};
3. Map dictionary = new Map();
4. Map dictionary = new Map.from({
      'apple':'사과',
      'banana':'바나나',
      });
      
 print(dictionary3);
 print(dictionary3.keys.toList()); // [apple, banana]
 print(dictionary3.values.toList()); // [사과, 바나나]

## Map 타입선언하기
```
void main(){
  Map<string, int> price = {
    'apple':2000,
    'banana':4000,
    'watermelon':6000,
    };
 }
```

🎊Map안에서 키는 유일해야한다, 같은 키가 여러개 존재 할 수 없다!!
