# PalindromeNumber

## Question
Given an integer x, return true if x is palindrome integer.

An integer is a palindrome when it reads the same backward as forward.

![image](https://user-images.githubusercontent.com/61695175/161005505-afd47f39-a0ec-49ee-9dfa-f2c13e7b3a45.png)

* 분기 처리 해주기
```javascript
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
    if(x<0){
        return false
    }

    return !!(x.toString().split('').join('') == x.toString().split('').reverse().join(''))
};
```
