# class 선언 및 constructor
##  class 선언하기
```
void main(){
  // OOP - Object Oriented Programming
  // 객체지향 프로그래밍
  
  Idol aespa = new Idol();
  Idol winter = new Idol('윈터', '에스파');
  
  // Instantiation  인스턴스화 
  // 함수를 변수로 변형하는 것
  aespa.sayName();
  
  print(winter.name) // 윈터
  print(winter.group) // 에스파
 
 // Map형태로 인자를 넘겨줍니다.
 Idol rm = new Idol.fromMap({
  'name':'RM',
  'group':'BTS',
 })
 
 rm.sayName() // 제 이름은 RM입니다.
 }
  
  class Idol {
    // 한번 선언되면 변경될 수 없습니다.
    final String name;
    String group;
    
    //외부에서 값을 받겠다. (constructor)
    Idol(
      String name,
      String group,
    ) : this.name = name, this.group = group;
    
    Idol.fromMap(
      Map input,
    ): this.name = input['name'],
       this. group = input['group']
    
    void sayName(){
      print('제 이름은 ${this.name}입니다');
    }
}
```

## Getter and Setter
```
void main() {
  // Getter => 값을 가져올때
  // Setter => 값을 변경할때

  Idol winter = new Idol(name: '윈터', group: '에스파');

  winter.sayName();

  print(winter._name);
  print(winter.name);
}

class Idol {
  // private variable
  String _name;
  String _group;

  Idol({
    String name,
    String group,
  })  : this._name = name,
        this._group = group;

  void sayName() {
    print('내 이름은 ${this._name} 입니다.');
  }

  get name {
    return this._name;
  }

  set name(String name) {
    this._name = name;
  }
}

```

## class inheritance
```
void main() {
  Idol winter = new Idol(name: '윈터', group: '에스파');

  winter.sayName();
  winter.sayGroup();
 
  BoyGroup rm = new BoyGroup('RM', 'BTS');
  print(rm.name);
  print(rm.group);
  rm.sayMale();
  
  GirlGroup wendy = new GirlGroup('웬디', '레드벨벳');
  wendy.sayFemale();
}

class Idol {
  String name;
  String group;

  Idol({
    String name = '',
    String group = '',
  })  : this.name = name,
        this.group = group;

  void sayName() {
    print('저는 ${this.name} 입니다');
  }

  void sayGroup() {
    print('저는 ${this.group}입니다');
  }
}

//extends - 상속 할때 사용
class BoyGroup extends Idol {
  BoyGroup(
    String name,
    String group,
  ) : super(name: name, group: group);
  
  void sayMale(){
    print('저는 남자 아이돌입니다.');
  }
}

//자식끼리는 상속되지 않고 부모에만 상속됩니다.
class GirlGroup extends Idol {
  GirlGroup(
  String name,
  String group,): super(name:name, group: group);
  
  void sayFemale(){
    print('저는 여자 아이돌입니다.');
  }
}
```

