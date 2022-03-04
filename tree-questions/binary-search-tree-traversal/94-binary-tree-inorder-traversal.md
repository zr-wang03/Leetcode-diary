# 94 Binary Tree Inorder Traversal

* Easy
* Given the `root` of a binary tree, return _the inorder traversal of its nodes' values_.
* [https://leetcode.com/problems/binary-tree-inorder-traversal/](https://leetcode.com/problems/binary-tree-inorder-traversal/)
* ![](<../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1).png>)

### Solution 1

Runtime: **32 ms**Memory Usage: **14.2 MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        resp=[]
        self._inorderTraversal(root,resp)
        return resp
        
    def _inorderTraversal(self,root,resp):
            if root:
                self._inorderTraversal(root.left,resp)
                resp.append(root.val)
                self._inorderTraversal(root.right,resp)
```

{% hint style="info" %}
This is an recursive approach.&#x20;
{% endhint %}

### Solution 2

Runtime: **28 ms**Memory Usage: **14.3 MB**

```
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        # left, root, right
        
        output = []
        def dfs(root, output):
            
            if root:
                
                if root.left:
                    dfs(root.left, output)
                output.append(root.val)
                if root.right:
                    dfs(root.right,output)
        
        dfs(root, output)
        return output
```

{% hint style="info" %}
This solution still uses recursive method but has been optimized so that redundant recursions are removed.&#x20;
{% endhint %}

### Solution 3

Runtime: **32 ms**Memory Usage: **14.3 MB**

```
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        resp,stack=[],[]
        while True:
            while root:
                stack.append(root)
                root=root.left
            if not stack:
                return resp
            node=stack.pop()
            resp.append(node.val)
            root=node.right
            

```

{% hint style="info" %}
This is the iterative solution using stack.&#x20;
{% endhint %}

### Solution 3'

```
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        resp,stack=[],[]
        while root or stack:
            if root:
                stack.append(root)
                root=root.left
            else:
                node=stack.pop()
                resp.append(node.val)
                root=node.right
        return resp
```

{% hint style="info" %}
There is not an optimized version of solution 3. But by merging two whiles into one, the code looks more elegant.&#x20;
{% endhint %}
