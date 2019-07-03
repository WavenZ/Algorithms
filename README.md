# Algorithms

Leecode记录

## 1. Two Sum
**题目：**\
Given an array of integers, return indices of the two numbers such that they add up to a specific target.\
You may assume that each input would have exactly one solution, and you may not use the same element twice.\
**样例:**
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

## 2. Add Two Numbers
**题目：**\
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.\
You may assume the two numbers do not contain any leading zero, except the number 0 itself.\
**样例:**
> Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
> Output: 7 -> 0 -> 8
> Explanation: 342 + 465 = 807.

**思路：**
由于输入链表的顺序是从低位到高位，因此可以像我们平时做加法那样从低位到高位进行求和，同时保存进位信息即可。

**代码：**
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int carry = 0, sum = 0, value = 0;
        ListNode* l3 = NULL;
        ListNode* p = l3;
        int val1 = l1->val;
        int val2 = l2->val;
        while(1){
            sum = val1 + val2 +carry;
            value = sum%10;
            carry = sum/10;
            ListNode* node = new ListNode(value);
            if(p == NULL) p = l3 = node;
            else{
                p->next = node;
                p = p->next;
            } 
            if(l1->next == NULL && l2->next == NULL && carry == 0) return l3;
            if(l1->next){
                l1 = l1->next;
                val1 = l1->val;
            }else val1 = 0;
            if(l2->next){
                l2 = l2->next;
                val2 = l2->val;
            }else val2 = 0;
        }
        return l3;
    }
};
```
