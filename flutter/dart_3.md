# final ,const, operators

변수값이 지정되었다면 변경 되지 않도록 합니다.
```
void main(){
  final String name = '코드팩토리';
  
  name = '에스파'; // Error 바뀔수없다
 }
```

## final vs const
```
void main(){
  final DateTime now = DateTime.now();
  // const DateTime now = DateTime.now(); ERROR
  // 컴파일시 DateTime.now()의 값을 알기 어렵기 떄문에 const로 저장할 수 없다.
  // But final은 컴파일 후 실행이 되는 순간에 지정되므로 사용 가능하다.
  print(now);
  
  //일초뒤에 실행해라 하는 함수
  Future.delayed(
    Duration(milliseconds: 1000),
    (){
    final DateTime now2 = DateTime.now();
     // const DateTime now2 = DateTime.now(); ERROR
    print(now2);
      }
    );
 }
```
일반적으로 final을 많이 사용합니다.

## operators ??= 
```
number2 ??= 4
// number2가 null이면 4을 넣어라
// null이 아니면 무시

int number3;
print(number3) // null

number3 ??= 4;
print(number3) // 4
```

## operators is
```
void main(){
  int number = 1;
  print(number is int); //true
  print(number is String); // false
}
```

