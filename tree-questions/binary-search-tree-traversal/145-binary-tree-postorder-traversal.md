# 145 Binary Tree Postorder Traversal

* Easy
* Given the `root` of a binary tree, return _the postorder traversal of its nodes' values_.
* [https://leetcode.com/problems/binary-tree-postorder-traversal/](https://leetcode.com/problems/binary-tree-postorder-traversal/)
* ![](<../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)

### Solution 1

Runtime: **20 ms** Memory Usage: **14.2 MB**

```
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        resp=[]
        def dfs(node):
            if node:
                if node.left:
                    dfs(node.left)
                if node.right:
                    dfs(node.right)
                resp.append(node.val)
                
        dfs(root)
        return resp
```

{% hint style="info" %}
Simple Recursive method
{% endhint %}

### Solution 2

Runtime: **28 ms** Memory Usage: **14.3 MB**

```
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        resp,stack=[],[root]
        while stack:
            node=stack.pop()
            if node:
                resp.append(node.val)
                if node.left:
                    stack.append(node.left)
                if node.right:
                    stack.append(node.right)
        return resp[::-1]
        
```

{% hint style="info" %}
This is an iterative method. It first go through the same process as Preorder Traversal, then reverse the output.&#x20;
{% endhint %}
