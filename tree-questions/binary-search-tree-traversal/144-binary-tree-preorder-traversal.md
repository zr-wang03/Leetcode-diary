# 144 Binary Tree Preorder Traversal

* Easy
* Given the `root` of a binary tree, return _the preorder traversal of its nodes' values_.
* [https://leetcode.com/problems/binary-tree-preorder-traversal/](https://leetcode.com/problems/binary-tree-preorder-traversal/)
* ![](<../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)

### Solution 1

Runtime: **32 ms**Memory Usage: **14.3 MB**

```
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        resp,stack=[],[root]
        while stack:
            node=stack.pop()
            if node:
                resp.append(node.val)
                stack.append(node.right)
                stack.append(node.left)
        return resp
```

{% hint style="info" %}
Iterative solution using the FILO trait of stacks.&#x20;
{% endhint %}

### Solution 2

Runtime: **32 ms**Memory Usage: **14 MB**

```
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        resp=[]
        def dfs(root):
            if root:
                resp.append(root.val)
                if root.left:
                    dfs(root.left)
                    
                if root.right:
                    dfs(root.right)
        dfs(root)
        return resp
```

{% hint style="info" %}
Simple recursive method&#x20;
{% endhint %}
