# House Robber
##


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
