
## romanToInt

### Question
![image](https://user-images.githubusercontent.com/61695175/161181656-2803046d-019b-4749-86f1-76db223b93b7.png)


#### 빅오 분석
O(n)

```javascript
/**
 * @param {string} s
 * @return {number}
 */
 var romanToInt = function(s) {
  let map = [];
  const TwoRoman = [    
    "IV",
    "IX",
    "XL",
    "XC",
    "CD",
    "CM",
  ]
  const Roman = {
    I: 1,
    V: 5,
    X: 10,
    L: 50,
    C: 100,
    D: 500,
    M: 1000,  
    IV: 4,
    IX: 9,
    XL: 40,
    XC: 90,
    CD: 400,
    CM: 900
  }

  const result = s.split('');
    for(let i =0; i<result.length; i++){
      if(TwoRoman.includes(result[i] + result[i+1])){
        map[i] = Roman[result[i]+ result[i+1]]
        i = i+1
      }else{
        map[i] = Roman[result[i]]
      }
    }
    return map.reduce((prev, curr)=> prev+curr,0)
  }
```

