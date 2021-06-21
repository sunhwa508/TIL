# Overriding, Static, this, super, interface, Cascade Operator
## class Method Overriding
```
void main() {
  // Method Overriding
  // Method 덮어쓰기
  
  Parent parent = new Parent(3);
  Child child = new Child(3);
  
  print(parent.calculate());
  print(child.calculate());
}

class Parent {
  final int number;

  Parent(
    int number,
  ) : this.number = number;

  // Function 함수
  // Method
  int calculate() {
    return this.number * this.number;
  }
}

class Child extends Parent {
  Child(
    int number,
  ) : super(
          number,
        );
  
  //decorator override라는 데코레이터를 활용해서 부모의 매소드를 덮어쓰기 할 수 있습니다.
  @override
  int calculate(){
    int result = super.calculate();
    
    return result+result;
  }
}

```

## class Static
```
void main() {
  Employee seulgi = new Employee('슬기');
  Employee chorong = new Employee('초롱');
  
  seulgi.printNameAndBuilding(); //제 이름은 슬기입니다.  " "건물에서 근무하고 있습니다.
  chorong.printNameAndBuilding(); //제 이름은 초롱입니다.  " "건물에서 근무하고 있습니다.
  
  Employee.building = '여의도 we work';
  
  seulgi.printNameAndBuilding(); //제 이름은 슬기입니다. 여의도 we work 건물에서 근무하고 있습니다.
  chorong.printNameAndBuilding(); //제 이름은 초롱입니다. 여의도 we work 건물에서 근무하고 있습니다.
  
  // 아무리 많은 인스턴스가 생성되더라도 static 키워드를 사용한다면 
  // 모든 인스턴스의 값을 한번에 바꿀 수 있습니다.
  Employee.building = '을지로 we work';
  
  seulgi.printNameAndBuilding(); //제 이름은 슬기입니다. 을지로 we work 건물에서 근무하고 있습니다.
  chorong.printNameAndBuilding(); //제 이름은 초롱입니다. 을지로 we work 건물에서 근무하고 있습니다.
  
}

// Static Keyword

// 직원
// 근무하고있는 건물 - 모든 직원이 다 같음
// 지원의 이름 - 사람마다 다 다름
class Employee{
    static String building = '';
    String name;
  
  Employee(
    String name,
  ): this.name = name;
  
  void printNameAndBuilding(){
    print('제 이름은 ${this.name}입니다. $building 건물에서 근무하고 있습니다.');
  }
}
```

## class Super 과 this
```
void main() {
  Engineer codeFactory = new Engineer(
      languages: ['dart', 'javascript'], name: '프론트몽키', building: '여의도 wework');

  print(codeFactory.name); // 프론트몽키
  print(codeFactory.building); // 여의도 wework
  print(codeFactory.languages); //[dart, javascript]
  
  codeFactory.sayInfo(); //저의 이름은 프론트몽키 입니다. 제가 근무하는 건물은 여의도 wework 입니다. 제가 사용할 수 있는 언어는dart, javascript
  codeFactory.sayName(); // this.name 은 프론트몽키, super.name 은 프론트몽키 입니다.
}
// 직원
class Employee {
  final String building;
  final String name;

  Employee(
    String building,
    String name,
  )   : this.building = building,
        this.name = name;
}

// 엔지니어
// 사용할줄 아는 언어 = 리스트로
class Engineer extends Employee {
  List<String> languages;
  //String name; 이값이 없을 경우 super.name을 상속받는다.
  
  Engineer({
    List<String> languages,
    String name,
    String building,
  })  : this.languages = languages,
        super(
          building,
          name,
        );

  void sayInfo() {
    print(
        '저의 이름은 ${super.name} 입니다. 제가 근무하는 건물은 ${this.building} 입니다. 제가 사용할 수 있는 언어는${this.languages.join(', ')}');
  }
  
  void sayName(){
    print('this.name 은 ${this.name}, super.name 은 ${super.name} 입니다.');
  }
}

```

## interface
```
void main() {
  BoyGroup bts = new BoyGroup('BTS');
  
  bts.sayName();
  
  GirlGroup redVelvet = new GirlGroup('레드벨벳');
  
  redVelvet.sayName();
  
}

// Interface
// 함수의 이름만 지정해줍니다.
class IdolInterface{
  String name;
  
  void sayName(){}
}
class BoyGroup implements IdolInterface{
  String name;
  
  BoyGroup(
  String name,
  ): this.name = name;
  
  void sayName(){
    print('제 이름은 ${this.name}입니다');
  }
  
}
class GirlGroup implements IdolInterface{
  String name;
  
  GirlGroup(
  String name,) :this.name = name;
  
  void sayName(){
    print('제 이름은 ${this.name}입니다.');
  }
}
```

## interface / inheritant
변수와 메소드를 강제했으면 좋겠다 extends => interface가 더 맞는 방향

## Cascade Operator
```
void main() {
  Idol idol = new Idol('슬기', '레드벨벳');

  idol.sayName();
  idol.sayGroup();

  //cascade로 불필요한 코드 줄이기
  new Idol('윈터', '에스파')
    ..sayName()
    ..sayGroup();
}

class Idol {
  String name;
  String group;

  Idol(String name, String group)
      : this.name = name,
        this.group = group;

  void sayName() {
    print('제 이름은 ${this.name} 입니다');
  }

  void sayGroup() {
    print('저는 ${this.group} 소속 입니다.');
  }
}
```
