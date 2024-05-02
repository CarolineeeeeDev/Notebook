# 动态规划DP

[TOC]



## 509. 斐波那契数

[509. 斐波那契数](https://leetcode.cn/problems/fibonacci-number/)

**斐波那契数** （通常用 `F(n)` 表示）形成的序列称为 **斐波那契数列** 。该数列由 `0` 和 `1` 开始，后面的每一项数字都是前面两项数字的和。也就是：

```
F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
```

给定 `n` ，请计算 `F(n)` 。

```c++
class Solution {
public:
    int fib(int n) {
        vector<int> dp(n+1);
        int sum;
        if (n==0)
        {
            return 0;
        }
        if (n==1)
        {
            return 1;
        }
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2 ; i<=n; i++)
        {
            sum = dp[0]+dp[1];
            dp[0] = dp[1];
            dp[1] = sum;
        }
        return sum;
    }
};
```



## 70. 爬楼梯

[70. 爬楼梯 - 力扣（LeetCode）](https://leetcode.cn/problems/climbing-stairs/description/)

假设你正在爬楼梯。需要 `n` 阶你才能到达楼顶。

每次你可以爬 `1` 或 `2` 个台阶。你有多少种不同的方法可以爬到楼顶呢？

 ```c++
 class Solution {
 public:
     int climbStairs(int n) {
         vector<int> dp(n+1);
         if (n==1)
         {
             return 1;
         }
         if (n==2)
         {
             return 2;
         }
         dp[1] = 1;
         dp[2] = 2;
         for (int i = 3; i<=n; i++)
         {
             dp[i] = dp[i-2] + dp[i-1];
         }
         return dp[n];
 
 
     }
 };
 ```



## 746. 使用最小花费爬楼梯

[746. 使用最小花费爬楼梯 - 力扣（LeetCode）](https://leetcode.cn/problems/min-cost-climbing-stairs/description/)

给你一个整数数组 `cost` ，其中 `cost[i]` 是从楼梯第 `i` 个台阶向上爬需要支付的费用。一旦你支付此费用，即可选择向上爬一个或者两个台阶。

你可以选择从下标为 `0` 或下标为 `1` 的台阶开始爬楼梯。

请你计算并返回达到楼梯顶部的最低花费。

```c++
#include <iostream>
using namespace std;

class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        vector<int> dp(cost.size()+1);
        dp[0] = 0;
        dp[1] = 0;
        for (int i = 2 ; i<= cost.size(); i++)
        {
            dp[i] = min(dp[i-1]+cost[i-1],dp[i-2]+cost[i-2]);
        }
        return dp[cost.size()];
    }
};
```



## 62. 不同路径

[62. 不同路径 - 力扣（LeetCode）](https://leetcode.cn/problems/unique-paths/description/)

一个机器人位于一个 `m x n` 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。

问总共有多少条不同的路径？

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m,vector<int>(n));
        for (int i = 0; i<m; i++)
        {
            dp[i][0] = 1;
        }
        for (int i = 0; i<n; i++)
        {
            dp[0][i] = 1;
        }
        for (int i =1; i<m; i++)
        {
            for (int j =1; j<n; j++)
            {
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
};
```



## 63. 不同路径II

[63. 不同路径 II - 力扣（LeetCode）](https://leetcode.cn/problems/unique-paths-ii/description/)

一个机器人位于一个 `m x n` 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用 `1` 和 `0` 来表示。

```c++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        vector<vector<int>> dp(m,vector<int>(n,0));
        for (int i =0; i<m && obstacleGrid[i][0]==0;i++)
        {
            dp[i][0] = 1;
        }
        for (int i =0; i<n && obstacleGrid[0][i]==0;i++)
        {
            dp[0][i] = 1;
        }
        for (int i = 1; i<m; i++)
        {
            for (int j = 1; j<n; j++)
            {
                if (obstacleGrid[i][j]==0)
                {
                    dp[i][j] = dp[i-1][j]+dp[i][j-1];
                }
            }
        }
        return dp[m-1][n-1];
    }
};
```



## 343.整数拆分

给定一个正整数 `n` ，将其拆分为 `k` 个 **正整数** 的和（ `k >= 2` ），并使这些整数的乘积最大化。

返回 *你可以获得的最大乘积* 。

**思路**：dp[i]是对i进行拆分，所得到的最大的乘积

遍历从1到i的情况，在j处进行拆分成两个数，得到乘积j*(i-j)。如果拆分成多个数，则得到乘积j * dp[i-j]

==固定j后，就已经将拆分j和i-j的所有情况都包含了==

```c++
class Solution {
public:
    int integerBreak(int n) {
        vector<int> dp(n+1);
        dp[0] = 0;
        dp[1] = 0;
        dp[2] = 1;
        for (int i = 3; i<=n; i++)
        {
            for (int j = 0; j<i; j++) //可以优化：j<i/2
            {
                dp[i] = max(j*(i-j),max(j*dp[i-j],dp[i]));//得到三个数的max值
            }
        }
        return dp[n];
    }
};
```



