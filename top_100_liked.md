# leetcode-snippet

* [543. Diameter of Tree](#543)


---

<a name="543"></a>
# 543. Diameter of Binary Tree
Q: Find the **diameter** (longest path) of a tree.
E.g.,

          1
         / \
        2   3
       / \     
      4   5    


Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

A:

![](https://i.imgur.com/FrEzcHW.png =200x)

```cpp
class Solution {
public:
    int diameterOfBinaryTree(TreeNode* root) {
        UpdateDiameterAndGetHeight(root);
        return diameter;
    }
        
private:
    int UpdateDiameterAndGetHeight(TreeNode* const pTreeNode){
        if(pTreeNode == nullptr){
            // Cannot get height for a nullptr, return -1
            return -1;
        }
        
        int lsh = UpdateDiameterAndGetHeight(pTreeNode->left);  // left subtree's height
        int rsh = UpdateDiameterAndGetHeight(pTreeNode->right); // right subtree's height
        
        if(lsh == -1 && rsh == -1){
            // Both children are empty
            return 0;
        }else if(lsh == -1 && rsh != -1){
            // Only exist left subtree
            diameter = max(diameter, rsh + 1);
            return rsh + 1;
        }else if(lsh != -1 && rsh == -1){
            // Only exist right subtree
            diameter = max(diameter, lsh + 1);
            return lsh + 1;
        }else{
            // Both exists
            diameter = max(diameter, rsh + lsh + 2);
            return max(lsh, rsh) + 1;
        }
    }

    int diameter = 0;
};
```
