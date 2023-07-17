---
{"dg-publish":true,"permalink":"/greedy/","dgPassFrontmatter":true,"noteIcon":""}
---

#greedy
```cpp
/*
 * @lc app=leetcode.cn id=45 lang=cpp
 *
 * [45] 跳跃游戏 II
 */
// @lc code=start
#include <bits/stdc++.h>
using namespace std;
class Solution
{
public:
    int jump(vector<int> &nums)
    {
        int max_far = 0; // 目前能跳到的最远位置
        int step = 0;    // 跳跃次数
        int end = 0;     // 上次跳跃可达范围右边界（下次的最右起跳点）
        for (int i = 0; i < nums.size() - 1; i++)
        {
            max_far = std::max(max_far, i + nums[i]);
            // 到达上次跳跃能到达的右边界了
            if (i == end)
            {
                end = max_far; // 目前能跳到的最远位置变成了下次起跳位置的有边界
                step++;        // 进入下一次跳跃
            }
        }
        return step;
    }
};
// @lc code=end
```
