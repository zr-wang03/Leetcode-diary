---
description: Two Points, Dictionary, Binary Search
---

# 167 Two Sum II - Input Array Is Sorted

* Easy
*   Given a **1-indexed** array of integers `numbers` that is already _**sorted in non-decreasing order**_, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

    Return_ the indices of the two numbers, _`index1`_ and _`index2`_, **added by one** as an integer array _`[index1, index2]`_ of length 2._
* __[_https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/_](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)__

### Solution 1

Runtime: **56 ms **Memory Usage: **14.5 MB**

```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        seen={}
        for index,value in enumerate(numbers):
            remain=target-value
            if remain in seen:
                return [seen[remain]+1,index+1]
            seen[value]=index
```

{% hint style="info" %}
This solution uses the same method of dictionary as the previous ones
{% endhint %}

### Solution 2

Runtime: **84 ms **Memory Usage: **14.6 MB**

```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        
        for index,value in enumerate(numbers):
            l, r = index+1, len(numbers)-1
            remain = target - value
            while l <= r:
                mid = l + (r-l)//2
                if numbers[mid] == remain:
                    return [index+1, mid+1]
                elif numbers[mid] < remain:
                    l = mid+1
                else:
                    r = mid-1
```

{% hint style="info" %}
This solution uses binary search. However this goes through the list multiple times if the answer we are looking for are at the last items.&#x20;
{% endhint %}

### Solution 3

Runtime: **64 ms **Memory Usage: **14.6 MB**

```
class Solution:
    def twoSum(self, numbers, target):
        low=0
        high=len(numbers)-1
        while low<high:
            if numbers[high]+numbers[low]<target:
                low+=1
            elif numbers[high]+numbers[low]>target:
                high-=1
            else:
                return low+1,high+1
```

{% hint style="info" %}
This uses two points method. Similar to the dictionary method, this solution should also only go through the list once. However, the dictionary method stops when it reaches the larger value of the two, while this solution stops when it reaches both values from both sides. Which of the two is faster depends on the list and the target.&#x20;
{% endhint %}
