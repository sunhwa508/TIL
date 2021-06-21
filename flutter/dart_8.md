#Cascade Operator
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
