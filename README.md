# Algorithms

Leecode记录

## 1. Two Sum
**题目：**
Given an array of integers, return indices of the two numbers such that they add up to a specific target.\
You may assume that each input would have exactly one solution, and you may not use the same element twice.\
**Example:**
> Given nums = [2, 7, 11, 15], target = 9,\
> \
> Because nums[0] + nums[1] = 2 + 7 = 9,\
> return [0, 1].

**思路：**
对数组进行遍历，用哈希表保存已经遍历过的数及其下标，对于当前迭代的数num，如果哈希表中已经存在target-num，则查找成功。

**代码：**
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hash;
        for(int i = 0; i < nums.size(); i++){
            if(hash.find(target - nums[i]) != hash.end()){
                vector<int> ret = {hash[target-nums[i]], i};
                return ret;
            }else hash[nums[i]] = i;
        }
        return {0, 0};
    }
};
```
