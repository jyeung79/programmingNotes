## Maximum Subarray problem
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

This can be solved by the Divide-And-Conquer O(n log(n)) or Dynamic Programming O(n).

DP solution: Use the Kadane algorithm
```javascript
let maxSubArray = (nums) => {

    // This include negative number already because it takes in the first value
    let subMax = nums[0];
    let absMax = nums[0];

    // Start at index 1 because you already stored the value of the
    // First element into subArrayMax and absoluteMax value already
    for (let i = 1; i < nums.length; i++) {
        subMax = subMax + nums[i];
        // Do you have to set subMax = 0 if the sum is negative?
        // I don't think we have to since it's doesn't matter
        subMax = subMax < nums[i] ? nums[i] : submax; // Change start = i if true
        // Simple way to use ternary operators to save the result of which is bigger into absMax
        absMax = absMax < subMax ? subMax : absMax; // Change end = i if true
    }
    return absMax;
}
```
[Code](https://www.techiedelight.com/maximum-subarray-problem-kadanes-algorithm/)
[Leetcode explanation](https://leetcode.com/problems/maximum-subarray/discuss/20193/DP-solution-and-some-thoughts)

