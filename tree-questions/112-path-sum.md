---
description: Recursive, Tree
---

# 112 Path Sum

* Easy
* Given the `root` of a binary tree and an integer `targetSum`, return `true` if the tree has a **root-to-leaf** path such that adding up all the values along the path equals `targetSum`.
* ![](<../.gitbook/assets/image (1).png>)here 7,2,1 are leaf because they don't have child node&#x20;
* [https://leetcode.com/problems/path-sum/](https://leetcode.com/problems/path-sum/)

### Solution 1

Runtime: **40 ms** Memory Usage: **15.1 MB**

```
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if root== None :
            return False
        targetSum-=root.val
        if root.left == None and root.right==None:
            if targetSum==0:
                return True
            else:
                return False
        return self.hasPathSum(root.left,targetSum)+ self.hasPathSum(root.right,targetSum)
```

{% hint style="info" %}
This method uses recursive method. Since we want to find a root-to-leaf path, we add an 'if' to determine if we have reached the leaf. If not, then we won't calculate the sum. ****&#x20;
{% endhint %}

### **Solution 2**

Runtime: **32 ms** Memory Usage: **15.2 MB**

```
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        self.res = False
        self.dfs(root, targetSum)
        return self.res 
    
    def dfs(self, root, target):
        if self.res:
            return 
        
        if not root:
            return 
        
        if root.left:
            self.dfs(root.left, target-root.val)
        if root.right:
            self.dfs(root.right, target-root.val)
        
        if not root.left and not root.right and target == root.val:
            self.res = True 
            return 
```

{% hint style="warning" %}
This one is faster than the previous solution. But I don't see the difference.
{% endhint %}
