#  List 심화
```
void main() {
  //Looping
  //Mapping
  //Reduce/Fold

  List<String> aespa = [
    '윈터',
    '카리나',
    '닝닝',
    '지젤',
  ];

  //Looping - forEach
  aespa.forEach((value) {
    print(value);
  });

  for (String value in aespa) {
    print(value);
  }

  //Mapping - map (새로운 리스트를 리턴합니다.)
  //Iterable<T> map<T>(T Function(String) f)
  final newList = aespa.map((value) {
    return '제 이름은 $value 입니다.';
  });

  print(newList); // Iterable 형태로 리턴해주지만 List로 받으려면 toList()함수 사용
  print(aespa); //원래의 리스트는 변경되지 않습니다.

  // Reduce/Fold - reduce, fold
  List<int> numbers = [
    0,
    1,
    2,
    3,
    4,
    5,
  ];

  int total = numbers.fold(0, (total, element) {
    return total + element;
  });
  print(total); //15

  int total2 = numbers.reduce((total, element) {
    return total + element;
  });
  print(total2);

  //fold와 reduce의 차이
  // fold를 사용하면 string값도 계산할 수 있습니다.
  List<String> names = ['프론트몽키', '트와이스', '에스파'];

  int total3 = names.fold(0, (total, element) {
    return total + element.length;
  });

  // allow function
  int total3 = names.fold(0, (total, element) => total + element.length);

  print(total3); // 12

  //아래같이 사용할 수 없다.
  //int total4 = names.reduce(total, element){
  //  return total + length.length;
  //};
}
```

#  Map 심화
```
void main() {
  Map map = {'Apple': '사과', 'Banana': '바나나', 'Kiwi': '키위'};
  print(map.keys); //(Apple, Banana, Kiwi)
  print(map.values); //(사과, 바나나, 키위)

  print(map.keys.toList()); //[Apple, Banana, Kiwi]
  print(map.values.toList()); //[사과, 바나나, 키위]

  //Mapping - map => (entry)
  final newMap = map.entries.map((entry) {
    final key = entry.key;
    final value = entry.value;

    return '$key 는 한글로 $value 입니다.';
  });

  print(newMap);

  //ForEach
  //Reduce/Fold

  map.entries.forEach((entry) {
    final key = entry.key;
    final value = entry.value;

    print('$key 는 한글로 $value 입니다.');
  });

  final total = map.entries.fold(0, (total, entry) {
    return total + entry.key.length;
  });

  print(total); //15

  List<int> numbers = [
    10,
    20,
    30,
    40,
    50,
  ];

  final newMap2 = numbers.map((item) {
    return '값이 $item 입니다.';
  });

  print(newMap2);

  final newMap3 = numbers.asMap();

  final newMap4 = numbers.asMap().entries.map((entry) {
    final index = entry.key;
    final value = entry.value;

    return 'index가 $index 일때 값은 $value 입니다';
  });

  print(newMap3);
  // {0: 10, 1: 20, 2: 30, 3: 40, 4: 50}
  print(newMap4);
  //(index가 0 일때 값은 10 입니다, index가 1 일때 값은 20 입니다, index가 2 일때 값은 30 입니다, index가 3 일때   값은 40 입니다, index가 4 일때 값은 50 입니다)
}
```
