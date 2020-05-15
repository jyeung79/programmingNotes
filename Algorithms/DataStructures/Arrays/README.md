# Array Problems

## Easy Problems
These are the easy array problems from leetcode.

### 1. Single Number

Give an array of non-empty integers, for every element appears twice except one, find that lone integer.

Real-life Example: You're in kindergarden and your teacher tells you to form pairs. Being the smart kid you are, you realize that in your class of odd numbered students, one will be left out. Your teacher hands each person a number with an exact number corresponding to it. You don't want to be alone so you figure out which number does not have a pair.

#### Brute force method

Loop twice where outer loop parses the array and inner loop looks for matches.

Time: O(n<sup>2</sup>) Not ideal
Space: O(1) because you don't have to store anything cus you return the integer
without a match

#### Hash Table

Time: O(n+n) because you do one loop to insert and one loop to lookup; Slower than Math Approach
Space: O(n) store the hash table

#### Math Method

$$
\sum TotalInts - \sum IntPairs = Lonely Integer
$$

In our code however, we don't have to sum all of the ints together. Just sum the ones if they appear in the hash table once and the rest that don't appear. Then if you subtract them the result is the number that does
not appear in the hash table which is the lone integer.

```javascript
    let singleNumber = (nums) => {
        // Time: O(n)
        // Space: O(n)
        
        let totalSum = 0, pairSum = 0;
        let hash = {};
        
        for (let i = 0; i < nums.length; i++) {
            if (!(nums[i] in hash)) {
                hash[nums[i]] = 1;
                totalSum += nums[i];
            } else {
                pairSum += nums[i];
            }
        }
        return totalSum - pairSum;
    };
```

#### XOR method

More ignenious is using bitwise operations. XOR all the numbers and you would return 1 int by itself.

$$
a \veebar 0 = a \quad a \veebar a = 0 \quad a \veebar b \veebar a = (a \veebar a \veebar b) = b
$$

```javascript
let singleNumber = (nums) => {
    // Time: O(n)
    // Space: O(1) Don't need to store anything
    
    return nums.reduce((sum, int) => sum^int);
};
```
---

### 2. Intersection of 2 Arrays

Given two arrays, write a function to compute their intersection.
Pretty Explanatory question; Nothing tricky about it.

```javascript
const intersect = (nums1, nums2) => {
    // Time: O(n + m) where n = nums1.length, m = nums2.length
    // Space: O(n + s) where s = set of nums1 & nums2
    let hash = {};
    let result = [];
    
    for (let i = 0; i < nums1.length; i++) {
        if (!(nums1[i] in hash)) {
            hash[nums1[i]] = 1;
        } else {
            hash[nums1[i]] += 1;
        }
    }
        
    for (let j = 0; j < nums2.length; j++) {
        if (nums2[j] in hash) {
            if (hash[nums2[j]] > 0) {
                result.push(nums2[j]);
                hash[nums2[j]] -= 1;
            }
        }
    }
    return result;
};
```

#### Followups
Answers from Discussion Page
1. What is the given array is already sorted?
   * Then instead you would have one looop to go through both arrays and compare the values
   * if nums1 < nums2 then increment nums1; nums1 > nums2 then increment nums2
   * if nums1 === nums2 then push it onto the result
2. What if nums 1 size is smaller than nums2's size?
   * We do a **binary search** on every element of nums1.
   * Each lookup is (log(n)) and if there is K number of elements in nums1 then time complexity is O(K log(n))
3. What if elements of nums2 are stored on disk, and the memory is limited so you can't load all elements
into the memory at once?
   * Map-reduce is a good answer. Open-ended.

Another answer from Discussion
1. Store the two strings in distributed system then use **MapReduce**
2. Process the strings by **chunk**, which fits the memory then deal with each chunk of data at a time
3. Process the strings by **stream**, then check

### 3. Remove Duplicates from Sorted Array

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Javascript makes this problem trivial because it has array methods such as splice which can insert/remove/modify the array in place without instantiating a new one. As such, you can just compare the current value to the next value until they are different. Afterwards, just increment your index and do the same until you reach the end of the array.

Assumptions: There are no undefined values in your array.

```javascript
const removeDuplicates = (nums) => {
    let i = 0;
    while (nums[i] !== undefined) {
        if (nums[i] === nums[i+1]) {
            nums.splice(i+1, 1);
        } else {
            i++;   
        }
    }
    return nums.length;
};
```

### 4. Best Time to buy and Sell Stock II

Say you have an array prices for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).


#### Brute Force method

The easiest method would be do use two loops and to caculate all possible combinations of maxprofit. This leads to O(n<sup>2</sup>) time complexity so its not optimal.

#### 4.1. Find the Max Differences

The maxprofit is just the sum of all the differences between a lower price and a higher price. Thus, all we need to is just sum all the price differences iff the prev price < current price.

```javascript
const maxProfit = (prices) => {
    let profit = 0;
    
    for (let i = 0; i < prices.length; i++) {
        if (prices[i] > prices[i-1]) {
            maxProfit += prices[i] - prices[i-1];
        }
    }
    return profit;
};
```
Time: O(n) - One Pass
Space: O(1)

#### 4.2. Find Valley and Peaks

The other method is to find the valleys and peaks and get the maxprofit from their sum. This case you iterate to look for the lowest value then iterate to look for the highest value. Then, subtract their difference to add to your maxProfit. Repeat until you reach the end of the array.

You only loop until ```i < prices.length - 1``` because you are compare your current value to the next value. Therefore, since you don't want to go out of bounds, you only loop until your 2nd last value.

To get your valleys, you compare your current to your next. If your current value is greater than your next, it means your current value is not at the valley. You iterate until you get your valley.

To get your peaks, you compare your current to your next. You stop iterating when you are at your peak value, ie. your current is greater than your next.

```javascript
const maxProfit = (prices) => {
    let profit = 0;
    let i = 0;
    let max = prices[0];
    let min = prices[0];

    while (i < prices.length - 1) {
        while (i < prices.length - 1 && prices[i] >= prices[i + 1]) {
            i++;
        }
        min = prices[i];
        while (i < prices.length - 1 && prices[i] <= prices[i + 1]) {
            i++;
        }
        max = prices[i];
        profit += max - min;
    }
    return profit;
}
```

### 5. Valid Sudoku

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

Each row must contain the digits 1-9 without repetition.
Each column must contain the digits 1-9 without repetition.
Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.

![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png "Valid Sudoku")

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

For this question you have to check for duplicate numbers in your row, column and sub-blocks. If you use a brute force method, you would have to use 3 for-loops to go through the entire sudoku to check for valid conditions.

It is easier to use a hashmap to store all the encountered values to check if there are duplicate numbers for the same row, column or sub-block. Because of a hashmap's O(1) insertion and search, it is optimal to retrieve and insert key-value pairs efficiently.

```javascript
const isValidSudoku = (board) => {
    let hash = {};
    
    for (let i = 0; i < 9; i++) {
        for (let j = 0; j < 9; j++) {
            let number = board[i][j];
            if (number !== '.') {
                const keyRow = `${number} in row ${i}`;
                const keyCol = `${number} in col ${j}`;
                const keyBlk = `${number} in ${Math.floor(i/3)}-${Math.floor(j/3)}`;
                console.log(number, keyRow, keyCol, keyBlk);
                
                if (hash[keyRow] || hash[keyCol] || hash[keyBlk]) {
                    return false;
                } else {
                    hash[keyRow] = true;
                    hash[keyCol] = true;
                    hash[keyBlk] = true;
                }
            }
        }
    }
    return true;
};
```

### 6. Move Zeroes

>Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

>Example:

>Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
Note:

You must do this in-place without making a copy of the array.Minimize the total number of operations.

Here what we do is to store the index of the value which was zero in ```idx```. When we reach a non-zero value, we then replace the zero at the ```idx``` with the non-zero value. We store a zero at the index of ```i``` but this value will be replaced later on with ```nums[i]``` as the loop iterates through the array. Last index only increments if the value is non-zero. 

```javascript
const moveZeroes = (nums) => {
    let lastIndex = 0;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== 0) {
            nums[lastIndex] = nums[i];
            nums[i] = lastIndex === i ? nums[i] : 0;
            lastIndex++;
        }
    }
};
```

## Medium

### 1. 3Sum

#### Brute-Force Method


#### [Two Pointers O(n<sup>2<sup>)](https://github.com/sahilbansal17/3Sum)

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
const threeSum = (nums) => {
    let result = [];
    let target = 0;
    let start = 0;
    let end = 0;
    let sum = 0;
    
    nums.sort((a, b) => a - b);
    console.log(nums);
    
    for (let i = 0; i < nums.length; i++) {
        target = nums[i];
        start = i + 1;
        end = nums.length - 1;
        
        while (start < end) {
            sum = nums[start] + nums[end];
            if (sum < -target) {
                start++;
            } else if (sum > -target) {
                end--;
            } else {
                result.push([target, nums[start], nums[end]]);
                let oldStart = start;
                let oldEnd = end;
                
                // Make sure your new start and new end !== prev index && start < end
                while (start < end && nums[start] === nums[oldStart]) {
                    start++;
                }
                while (end > start && nums[end] === nums[oldEnd]) {
                    end--;
                }
            }
        }
        while (i + 1 < nums.length && nums[i+1] === nums[i]) {
            i++;
        }
    }
    return result;
};
```

### 2. Longest Palindromic Substring

There are multiple approaches to the problem. First the brute force method is to pick all possible starting and ending positions for a substring, then verify it as a palindrome. O(n<sup>3</sup>) Other approaches include longest common substring, dynamic programming but these take O(n<sup>2</sup>) space complexity. The better approach at O(n<sup>2</sup>) time complexity and O(1) space complexity is Expand around the center.

#### Expand around the center

Palindrome mirrors around its center. There are 2n - 1 centers in a string. That is because a string ```abba``` has a center between the two bb's. Here you check palindromic substring starting at each char of a string.

```javascript
const longestPalindrome = (s) => {
    let start = 0;
    let end = 0;

    for (let i = 0; i < s.length; i++) {
        let left = i;
        let right = i;
        
        while (left >= 0 && s[left] === s[i]) {
            left--;
        }
        
        while (right < s.length && s[right] === s[i]) {
            right++;
        }
        
        while (left >= 0 && right < s.length && s[left] === s[right]) {
            left--;
            right++;
        }
        
        left += 1; // end does not need decrement b/c slice is to index end - 1
        if (end - start < right - left) {
            start = left;
            end = right;
        }
    }
    return s.slice(start, end);
}
```