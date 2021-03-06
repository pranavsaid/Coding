# LC312. Burst Balloons

### LeetCode

## Question

Given n balloons, indexed from 0 to n-1. Each balloon is painted with a number on it represented by array nums. You are asked to burst all the balloons. If the you burst balloon i you will get nums[left] * nums[i] * nums[right] coins. Here left and right are adjacent indices of i. After the burst, the left and right then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

**Note:** 

1. You may imagine nums[-1] = nums[n] = 1. They are not real therefore you can not burst them.
2. 0 ≤ n ≤ 500, 0 ≤ nums[i] ≤ 100

**Example:**

```
Given [3, 1, 5, 8]
Return 167
    nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
   coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167
```

## Solutions

### Solution 1

* C++
```
int maxCoins(vector<int>& nums) {
    int n = nums.size();
    nums.insert(nums.begin(), 1);
    nums.push_back(1);
    int dp[n+2][n+2] = {0};
    for(int len=1; len<=n; ++len)
        for(int left=1; left<=n-len+1; ++left)
            for(int mid=left, right=left+len-1; mid<=right; ++mid)
                dp[left][right] = max(dp[left][right], nums[left-1]*nums[mid]*nums[right+1] + dp[left][mid-1] + dp[mid+1][right]);
    return dp[1][n];
}
```

* Java
```
public int maxCoins(int[] nums) {
    int n = nums.length;
    int[] input = new int[n + 2];
    for (int i = 1; i <= n; i++)
        input[i] = nums[i - 1];
    input[0] = input[n + 1] = 1;
    
    int[][] dp = new int[n + 2][n + 2];
    
    for (int len = 1; len <= n; len++) {
        for (int i = 1; i <= n - len + 1; i++) {
            int j = i + len - 1;
            for (int mid = i; mid <= j; mid++) {
                dp[i][j] = Math.max(dp[i][j], dp[i][mid - 1] + dp[mid + 1][j] + input[i - 1] * input[mid] * input[j + 1]);
            }
        }
    }
    
    return dp[1][n];
}
```

`dp[i][j]` is to represent the maximum coins you can collect by bursting from i<sup>th</sup> to j<sup>th</sup> balloons.

`len` is the width from i<sup>th</sup> to j<sup>th</sup> balloons.

**Complexity:**

* **worst-case time complexity:** O(n<sup>3</sup>), where `n` is the length of `nums`.
* **worst-case space complexity:** O(n<sup>2</sup>), where `n` is the length of `nums`.


