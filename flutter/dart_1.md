# Dart 왕초보

[Dart pad](https://dartpad.dartlang.org/)
위 링크에서 다트언어를 연습할 수 있습니다. 

### console.log 찍기
![image](https://user-images.githubusercontent.com/61695175/122336523-f5fd2d00-cf77-11eb-9995-13b921fddc68.png)

### 변수 선언
![image](https://user-images.githubusercontent.com/61695175/122349857-9d359080-cf87-11eb-8039-c67e6a77febe.png)

### Number / boolean / string
```
void main(){
  int number = 1;
  print(number); // 1
  
  bool isTrue = true";
  print(isTrue); //true
  
  String name = "프론트몽키"; 
  String sentence = "는 동물이 아닙니다";
  
  print(name + sentence);
  // 프론트몽키는 동물이 아닙니다.
  print('$name$sentence'); //$사인이 붙으면 변수로 인식합니다.
  // 프론트몽키는 동물이 아닙니다.
}
```
###  Var, Dynamic 타입
Dynamic에서는 모든 타입값들이 들어올 수 있습니다.
```
void main(){
  dynamic name = "프론트몽키";
  
  print(name);
  
  name = 2;
  
  print(name);
}
```

###  List 타입
리스트를 선언하는 방법에는 2가지가 있다.
```
void main(){
  List redVelvetList = [];
  
  print(redVelvetList); //[]
  
  List redVelvetList2 = new List()

  print(redVelvetList2); //[]
  
  redVelvetList.add('슬기');
  redVelvetList.add('웬디');
  redVelvetList.add('조이');
  
  print(redVelvetList) //[슬기, 웬디, 조이]
  
  redVelvetList.removeAt(1);
  print(redVelvetList) //[슬기, 조이]
  
  List<String> btsList = new List(3)
  
  print(btsList);
  btsList.add('뷔'); //Error
  
  btsList[0] = '뷔' 
  btsList[1] = 'RM' 
  btsList[2] = '제이홉'
  
  print(brtList); // [뷔, RM, 제이홉]
  
}
```
