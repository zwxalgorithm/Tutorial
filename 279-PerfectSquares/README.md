## 题目分析
有一个正整数`n`，找到一系列的完全平方数（比如，`1,4,9,16,...`），它们的和为`n`，并且这些完全平方数的数量最少，返回完全平方数的最少数量。  
比如说，`n = 12`，`12 = 4 + 4 + 4`，完全平方数的最少数量为`3`；  
`n = 13`，`13 = 4 + 9`，完全平方数的最少数量为`2`。

## 题解
### 解题思路
直接的想法是遍历所有可能的完全平方数，比如`n = 23`，
- 先找离`23`最近的完全平方数`16`，则`23 = 7 + 16`，继续寻找子问题的解（子问题是`n = 7`时，最少的完全平方数的数量：`7=4+1+1+1`，数量为`4`），这种情况下和为`23`的完全平方数的数量是`5`；
- 再找完全平方数`9`，则`23 = 14 + 9`，继续寻找子问题的解（子问题是`n = 14`时，最少的完全平方数的数量：`14=1 + 4 + 9`，数量为`3`），这种情况下和为`23`的完全平方数的数量是`4`；
- 再找完全平方数`4`，则`23 = 19 + 4`，继续寻找子问题的解（子问题是`n = 19`时，最少的完全平方数的数量：`19=1 + 2 + 16`，数量为`3`），这种情况下和为`23`的完全平方数的数量是`4`；
- 再找完全平方数`1`，则`23 = 22 + 1`，继续寻找子问题的解（子问题是`n = 22`时，最少的完全平方数的数量：`22=4 + 9 + 9`，数量为`3`），这种情况下和为`23`的完全平方数的数量是`4`；
- 综上，`n = 23`时，完全平方数的最少数量是`4`。

求解上述例子时，有一个前提假设：小于`n`的正整数的完全平方数的最少数量是已知的。  
即，整数`n`的完全平方数最少数量可以通过小于`n`的结果得到，满足动态规划的条件。  
**状态转移方程**  
`dp[i]`表示整数`i`的完全平方数的最少数量。  
`dp[i]=min{ dp[i-j*j] + 1 | j >= 1 and j*j <= i }`。  

具体实现在`solution.cpp`中。  

**时间复杂度**  
`M_i`为小于或等于正整数`i`的完全平方数的数量，对于每个小于`n`的正整数都要判断`M_n`次，因此时间复杂度为`O(n * M_n)`，而`M_n = 根号n向下取整`，因此时间复杂度为`O(n^(3/2))`。

### 求解过程
`n = 23`，假设`1...22`的结果都已经计算出来。  
`dp[23] = min(dp[23-1*1], dp[23-2*2], dp[23-3*3], dp[23-4*4]) + 1 = 1 + min(dp[22], dp[19], dp[14], dp[7]) = 1 + min(3, 3, 3, 4) = 4`。