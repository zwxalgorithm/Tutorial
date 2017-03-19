### 题意
**中文描述**  
给定一个包含n个整数的数列S, 从数列中找出三个数的和与给定的target值最接近，返回这三个数的和。可以假定每组数有且只有一个答案。 

### 题解
**算法及复杂度(13 ms)**  
本题与第15题（[3Sum ](https://leetcode.com/problems/3sum/#/description)）十分类似，从题目上就可以看出来，第15题是求三个数和为0，而本题是求三个数和最接近target。  
本题采用和第15题同样的思路进行求解，先对数组进行排序，然后设置一重循环使用i进行对第一个数的迭代，然后分别设置left和right指针，寻找所有的情况，判断三个数的和最接近target的值。  
本题完全可以对第15的代码进简单修改进行本题的求解: 只需将后两个数的和为第一个数的相反数部分改为target与第一个数的差，然后把判断条件改为判断三个数与target的差的绝对值即可.算法思路及正确性可参考第15题题解。  
时间复杂度: O(n^2)，排序时间复杂度为O(nlogn)，求解的时间复杂度为O(n^2)，总的时间复杂度为两者的和取最高量级。    
代码参见同文件夹solution.cpp

### 算法正确性
**举个例子**  

    ```
    //输入数据
    nums = [4,2,3,1], target = 5
    //排序
    [1,2,3,4]
    
    //i = 0 时, j = 1, k = 3, 初始化ans = 1 + 2 + 3 = 6
    nums[i] = 1, targetjk = 5 - 1 = 4
    此时num[j] + num[k] = 6 > 4, sum = num[i] + num[j] + num[k] = 7, ans不更新, 需要减小k, k = 2
    此时num[j] + num[k] = 5 > 4, sum = 6, ans不更新, 需要减小k, k = 1
    此时j !< k,需要增加i, i = 1
    //i = 1时, j = 2, k = 3
    num[i] = 2, targetjk = 5 - 2 = 3
    此时num[j] + num[k] = 7 > 3，sum = 9, ans不更新, 需要减小,, k = 2
    此时j !< k，需要增加i,i = 2
    //i = 2时，i !< nums.size() - 2，结束运算, 返回结果ans = 6
    ```