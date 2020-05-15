# String Problems

## Easy Problems

### 1. Reverse String



Using javascript's Array prototype methods

```javascript
let reverseString = (s) => {
    return s.reverse();
};
```

If we cannot use javascript's inbuilt array prototype methods, we can have two pointers to switch values.
Here we set one pointer (i) to point at the beginning of the array and one (j) at the end. We use a temporary
variable to store the value of s[i] and then swap the values in the array. We stop when either the pointer (i) passes or is equal to the pointer (j).

```javascript
const reverseString = (s) => {
    let i = 0;
    let j = s.length - 1;
    let temp = "";
    
    while (i < j) {
        temp = s[i];
        s[i] = s[j];
        s[j] = temp;
        i++;
        j--;
    }
    return s;
};
```

Another methods is to use the recursion method. It's still in-place because you don't use any other data structure however, you have O(N) recursion stack. 

![data structure](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/Figures/344/stack2.png)

Understand the difference in post increment and pre increment. Post increment (i++) means that the value is read without the increment/decrement in place. Pre increment (++i) means that the value is incremented then read. Pretty smart use of pre and post increment/decrement. [stackoverflow](https://stackoverflow.com/questions/2371118/how-do-the-post-increment-i-and-pre-increment-i-operators-work-in-java)

``` javascript
let j = 5;
let a = j++ + ++j + j++;
//  a = 5 + 7 + 7;
// 1st step: j++ => 5 because it increments afterwards
// 2nd step: ++j => 7 because it was incremented by j++ then preincrement by ++j
// 3rd step: j++ => 7 same idea as 1st step
// a = 19, j = 8
```

A blank return statement transfers the control back to the calling function. [stackoverflow](https://stackoverflow.com/questions/3717420/is-there-a-benefit-to-using-a-return-statement-that-returns-nothing)

```javascript
const reverseString = (s) => {
    helperReverse(s, 0, s.length -1);
};

const helperReverse = (s, left, right) => {
    if (left > right) return;
    const temp = s[left];
    s[left++] = s[right];
    s[right--] = temp;
    helperReverse(s, left, right);   
};
```
### 2. Reverse Integer

Not really the case in javascript but the algorithm goes as such:

Change the number into a string then an array of characters. Reverse the characters before joining it together. Remove all 0s in front with regex and multiply by the sign again.

Lastly check if the result is within the bounds of a 32 bit signed integer.

```javascript
let reverse = (x) => {
    const MAXINT = 2**31 - 1;
    const MININT = -(2**31);
    let neg = x < 0 ? -1 : 1;
    
    let result = Math.abs(x).toString().split('').reverse().join('').replace(/^0*/, '') * neg;
    
    return result = result > MAXINT || result < MININT ? 0 : result;
};
```

### 3. Valid Palindrome

The easiest way to check if a string is a valid palindrome is to have two pointers, one at the start of the string and one at the end. Each iteration you would compare if the ```char[start] === char[end]```. Afterwards you would increment start and decrement end to compare your next pair of characters.

To combat the issue of checking for alphanumeric chars, first set the new string as lowercase then replace all non-word characters ```\W - non word``` (```\w - word```) and replace it all with empty string, ''. This is done using Regex or regular expression which is used for string searching or matching.

```javascript
const isPalindrome = (s) => {
    let alphaNum = s.toLowerCase().replace(/[\W]/g, '');
    let start = 0;
    let end = alphaNum.length - 1;
    
    for (; start < end; start++, end--) {
        if (alphaNum[start] !== alphaNum[end]) {
            return false;
        }
    }
    return true;
};
```

### 4. Count and Say

>Write a code to do following:</br>
Given an integer n where 1 ≤ n ≤ 30, generate the nth term of the count-and-say sequence. You can do so recursively, in other words from the previous member read off the digits, counting the number of digits in groups of the same digit.

Count and Say Sequence
```javascript
1                       // n = 1
11                      // n = 2
21                      // n = 3
1211                    // n = 4
111221                  // n = 5
312211                  // n = 6
13112221                // n = 7
1113213211              // n = 8
31131211131221          // n = 9
13211311123113112211    // n = 10
...
```

This problem can be quite tricky as the ```n```<sup>th</sup> term requires all the previous ```n - 1``` terms beforehand. First this isn't a dynamic programming problem because each subsequent term must rely only on the previous term to generate the new sequnces. Memoization is not applicable.

In this case, we must generate all the terms leading up to ```n - 1``` to calculate each subsequent term until we get the ```n```<sup>th</sup> term. The outer while loop goes through ```n - 1``` times to get each term. Then for each termn we loop through the sequences to get the count. Afterwards appending the results to the output string.



```javascript
function countAndSay(n) {
    let result = "1";
    let i = 1;
 
    while (i < n) {
        let output = '';
        let count = 1;
        for (let j = 1; j < result.length; j++) {
            if (result[j] === result[j - 1]) {
                count++;
            } else {
                output += count;
                output += result[j - 1];
                count = 1;
            }
        }
        output += count;
        output += result[result.length - 1];
        result = output;
        i++;
    }
 
    return result;
};
```

Time: O(mn) - m is the length of the char sequence and n is the term of the sequence

Space: O(1) - only constant space required

