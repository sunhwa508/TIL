# typedef 
```
void main(){
  add(1,2);
  subtract(3,2);
  
  Operation oper = add;
  
  oper = subtract;
  
  oper(3,2) //x 빼기 y는 1 입니다.
}
typedef Operation(int x, int y);

void add(int x, int y){
  print('x 더하기 y는 ${x+y}입니다');
}

void subtract(int x, int y){
  print('x 빼기 y는 ${x-y}입니다');
}
```


```
void main(){
  calculate(1, 2, add); //x 더하기 y는 3 입니다.
  calculate(1, 2, subtract); //x 빼기 y는 -1 입니다.
}

typedef Operation(int x, int y);

void add(int x, int y){
  print('x 더하기 y는 ${x+y}입니다');
}

void subtract(int x, int y){
  print('x 빼기 y는 ${x-y}입니다');
}

void calculate(int x, int y, Operation oper){
 oper(x,y);
}
```
> 자주쓰이지는 않지만 가끔 활용하면 코드를 단축 할 수 있습니다~
