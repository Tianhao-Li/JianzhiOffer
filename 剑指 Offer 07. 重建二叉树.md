# 剑指 Offer 07. 重建二叉树

## Description

输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

 

示例 1:


Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
示例 2:

Input: preorder = [-1], inorder = [-1]
Output: [-1]


限制：

0 <= 节点个数 <= 5000



## Solution

> PreOrder for root, InOrder for subtree size

```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        // Get root from preorder, then get left & right subtree size from inorder (use a map to find the root), get elements of subtrees from preorder

        // 1. Turn inorder into a map
        Map<Integer, Integer> inMap = getMap(inorder);

        // 2. Use recursion to reconstruct the tree
        return reconstruct(inMap, 0, inorder.length - 1, preorder, 0, preorder.length - 1);
    }

    // Helper function: reconstruct the given range of the tree, return its root
    private TreeNode reconstruct(Map<Integer, Integer> inMap, int inLeft, int inRight, int[] preorder, 
                                int preLeft, int preRight) {
        // Left & Right inclusive (also includes the root) -- here it is the index                            
        // Base case
        if (inLeft > inRight) {
            return null;
        }

        TreeNode root = new TreeNode(preorder[preLeft]);
        int leftSize = inMap.get(root.val) - inLeft;

        root.left = reconstruct(inMap, inLeft, inMap.get(root.val) - 1, preorder, preLeft + 1, preLeft + leftSize);
        root.right = reconstruct(inMap, inMap.get(root.val) + 1, inRight, preorder, preLeft + leftSize + 1, preRight);

        return root;
    }
 
    private Map<Integer, Integer> getMap(int[] inorder) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }

        return map;
    }
}
```

- TC: O(n)
- SC: O(n)