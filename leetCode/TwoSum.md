
## TwoSum

### Question
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

![image](https://user-images.githubusercontent.com/61695175/161002977-29be7a0b-6692-4d06-af41-e89768a39239.png)


> 계산되어야 하는 배열을 생각해보고 코드로 옮기기 
```
 [0,1][0,2][0,3]
 [1,2][1,3]
 [2,3]
```

```javascript
var twoSum = function(nums, target) {
    for(let i=0; i<nums.length;i++){
       for(let j=i+1; j<nums.length; j++){
           if(nums[i]+nums[j] === target){
               return [i,j]
           }
       }
    }
};
```
