---
description: Dictionary
---

# 1 Two sums

* Easy
* Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.
* [https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/)

### 1. Solution one&#x20;

Runtime: **4116 ms **Memory Usage: **14.8 MB**

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if nums[i]+nums[j]==target:
                    return [i,j]
```

{% hint style="info" %}
This solution goes over every two combinations of the list. Therefore it takes much longer time&#x20;
{% endhint %}

### 2. Solution two&#x20;

Runtime: **55 ms **Memory Usage: **15.4 MB**

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        seen={}
        for index,value in enumerate(nums):
            remain=target-value
            if remain in seen:
                return [seen.get(remain),index]
            seen[value]=index
```

{% hint style="info" %}
By creating a dictionary and storing the values already seen the program only has to go through the list once
{% endhint %}

##

##
