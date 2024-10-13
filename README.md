# House Robber
## https://leetcode.com/problems/house-robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

``` 
Example 1:

Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
Example 2:

Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
``` 

**Constraints:**

1. 0 <= nums.length <= 100
2. 0 <= nums[i] <= 400

### Approach :
Since we can't rob two adjacent houses, we have either of 3 choices.
1. Rob odd houses e.g.  1, 3, 5, 7, ... , odd house
2. Rob even houses  e.g. 2, 4, 6, 8, ... , even house
3. Rob houses in any random order(but don't rob two adjacent houses) e.g. (1, 4, 7, ..., 10) or (2, 5, 8, 11, 14)

Its clear that we don't know which sequence will give us the most amount of money. 
We could try all possible sequences and find out the max amount of money we can rob.
But that will be a naive solution and running time will not be very good.

#### Dynamic Programming to the rescue (This solution will also work if input array contains negative numbers)
At each house we have two choices : 
1. Rob the ith house (money from ith house and total money collected till house i-2)
2. Don't rob the ith house (total money collected till house i-1)

# Implementation 1 : O(n) Space
```java
class Solution {
    public int rob(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        if(nums.length == 1)
            return nums[0];
        if(nums.length == 2)
            return Math.max(nums[0], nums[1]);
        
        int[] dp = new int[nums.length];
        dp[0] = nums[0]; dp[1] = Math.max(nums[0], nums[1]);
        for(int i = 2; i < nums.length; i++) {
            dp[i] = Math.max(nums[i] + dp[i-2], dp[i-1]);
        }
        return dp[nums.length-1];
    }
}
```
# Implementation 2 : O(1) Space
```java
class Solution {
    public int rob(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        if(nums.length == 1)
            return nums[0];
        if(nums.length == 2)
            return Math.max(nums[0], nums[1]);
        
        int maxBeforeTwoHouse = nums[0];
        int maxBeforeOneHouse = Math.max(nums[0], nums[1]);
        int maxAtI = Math.max(nums[0], nums[1]);
        
        for(int i = 2; i < nums.length; i++) {
            maxAtI = Math.max(maxBeforeTwoHouse+ nums[i] , maxBeforeOneHouse);
            maxBeforeTwoHouse = maxBeforeOneHouse;
            maxBeforeOneHouse = maxAtI;
        }
        return maxAtI;
    }
}
```


# References :
https://www.youtube.com/watch?v=xlvhyfcoQa4
