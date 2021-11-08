# 653 Two Sum IV - Input is a BST

* Easy
* Given the `root` of a Binary Search Tree and a target number `k`, return _`true` if there exist two elements in the BST such that their sum is equal to the given target_.
* [https://leetcode.com/problems/two-sum-iv-input-is-a-bst/](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/21/sum\_tree\_1.jpg)

```
Input: root = [5,3,6,2,4,null,7], k = 9
Output: true
```

### Solution 1

Runtime: **116 ms **Memory Usage: **17.3 MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def findTarget(self, root: Optional[TreeNode], k: int) -> bool:
        
        if not root:
            return False
        
        return self._findTarget([],root,k) 
    
    def _findTarget(self,nodelist,root: Optional[TreeNode],k):
        if not root:
            return
        remain=k-root.val
        if remain in nodelist: 
            return True
        nodelist.append(root.val)
        
        return self._findTarget(nodelist,root.left,k) or self._findTarget(nodelist,root.right,k)
```

{% hint style="info" %}
This solution uses recursive method to search through the tree. Then creates a list like the one in '1 Two sums' to identify if two sums fits the need.&#x20;
{% endhint %}

### Solution 2

Runtime: **68 ms **Memory Usage: **18.1 MB**

```
class Solution:
    def findTarget(self, root: Optional[TreeNode], k: int) -> bool:
        seen=set() 
        def findfunction(root):
            if root:
                if k-root.val in seen:
                    return True
                seen.add(root.val)
                return (findfunction(root.left) or findfunction(root.right))
        return findfunction(root)
```

{% hint style="info" %}
Since we don't care about the sequence in the 'seen' list, we can optimize and replace it with set or dictionary. &#x20;
{% endhint %}
