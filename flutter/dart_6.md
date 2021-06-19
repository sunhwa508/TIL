# class 선언 및 constructor
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
