# for, while문 / Enum 타입

## for
```
void main(){
  List members = [
  1,
  1,
  2,
  3,
  5,
  8,
  ];
  
  int total = 0;
  for(int number in numbers){
    total += number;
    }
    
    print(total)
  }
```

## while
```
void main(){
  int number = 10;
  
  while(number<20){
  print(number);
  
  number++;
  }
 }
```

## Enum
```
enum Status{
  approved,
  rejected,
  pending,
  }

void main(){
  //승인 - approved
  //반려 - rejected
  //대기 - pending
  
  //String status = 'approved';
  Status status = Status.approved
  if(status == Status.approved){
    print('승인되었습니다')
   }else{
    print('반려되었습니다')
   }
}
```
> 오타에 대한 위험성을 적게 만들수 있습니다.
