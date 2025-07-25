# 二叉树part01

https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

## 二叉树的种类

### 满二叉树

满二叉树：一棵二叉树只有度为0的结点和度为2的结点，并且度为0的结点在同一层上

<img width="900" height="712" alt="image" src="https://github.com/user-attachments/assets/bcc70cd0-241e-47be-80f3-a3671694b118" />

这棵二叉树为满二叉树，也可以说深度为k，有2^k-1个节点的二叉树。

### 完全二叉树

完全二叉树的定义如下：除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层（h从1开始），则该层包含 1~ 2^(h-1) 个节点。

<img width="1426" height="670" alt="image" src="https://github.com/user-attachments/assets/3e26de1c-347a-4d79-badc-fb3a796d4526" />

### 二叉搜索树

二叉搜索树是有数值的，二叉搜索树是一个有序树:
- 若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值
- 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值
- 它的左、右子树也分别为二叉排序树

<img width="786" height="276" alt="image" src="https://github.com/user-attachments/assets/346f72d2-a999-413e-9c98-7cfdec962ef9" />

### 平衡二叉搜索树

平衡二叉搜索树：又被称为AVL（Adelson-Velsky and Landis）树，且具有以下性质：它是一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。

<img width="1410" height="384" alt="image" src="https://github.com/user-attachments/assets/5f519cbe-bb43-49a6-980d-6cbb19dddaba" />

## 二叉树的存储方式

二叉树可以链式存储，也可以顺序存储 (链式存储方式就用指针， 顺序存储的方式就是用数组。)

### 链式存储

链式存储如图：

<img width="1352" height="864" alt="image" src="https://github.com/user-attachments/assets/c509bf42-5775-415c-a675-2db70838ce98" />

### 顺序存储

顺序存储(用数组来存储二叉树)如图：

<img width="954" height="842" alt="image" src="https://github.com/user-attachments/assets/73d753db-4f06-49fe-83a4-68ca2bb3ada6" />

如果父节点的数组下标是 i，那么它的左孩子就是 i * 2 + 1，右孩子就是 i * 2 + 2。

## 二叉树的遍历方式

二叉树主要有两种遍历方式：
- 深度优先遍历：先往深走，遇到叶子节点再往回走。
- 广度优先遍历：一层一层的去遍历。

深度优先遍历：
  - 前序遍历（递归法，迭代法）中左右
  - 中序遍历（递归法，迭代法）左中右
  - 后序遍历（递归法，迭代法）左右中
<img width="1352" height="490" alt="image" src="https://github.com/user-attachments/assets/394e7710-1d39-4850-9574-ff2fdff458d1" />

经常会使用递归的方式来实现深度优先遍历

广度优先遍历：
  - 层次遍历（迭代法）

## 二叉树的定义

链式存储的二叉树节点的定义方式 C++:
```javascript
function TreeNode(val, left, right) {
    this.val = (val===undefined ? 0 : val)
    this.left = (left===undefined ? null : left)
    this.right = (right===undefined ? null : right)
}
```

##  递归遍历 （必须掌握）

文章链接：https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%80%92%E5%BD%92%E9%81%8D%E5%8E%86.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC

视频链接：https://www.bilibili.com/video/BV1Wh411S7xt


递归算法的三个要素:
1. 确定递归函数的参数和返回值
2. 确定终止条件
3. 确定单层递归的逻辑

### 144. Binary Tree Preorder Traversal

https://leetcode.com/problems/binary-tree-preorder-traversal/

Method 1 (更易懂): 

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var preorderTraversal = function(root) {
    // 存放前序遍历结果
    var res = [];

    // 二叉树遍历函数
    var traverse = function(root) {
        if (root == null) {
            return;
        }
        // 前序位置
        res.push(root.val);
        traverse(root.left);
        traverse(root.right);
    };

    traverse(root);
    return res;
};
```

Method 2: 

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var preorderTraversal = function(root) {
    // 如果 root 不为空（即当前节点存在），就执行中序遍历：
      //  先访问当前节点的值：root.val
      //  然后递归遍历左子树：preorderTraversal(root.left)
      //  最后递归遍历右子树：preorderTraversal(root.right)
      // 并将三个部分组合为一个数组返回。
    // 如果 root 是 null（即当前节点不存在），就返回一个空数组 []。
    //  通过展开运算符...把所有子结果拼接为一个数组
    return root ? [
        // 前序遍历：中左右
        root.val, // 中
        ...preorderTraversal(root.left), // 左
        ...preorderTraversal(root.right), // 右
    ]:[];
};
```

### 145. Binary Tree Postorder Traversal

https://leetcode.com/problems/binary-tree-postorder-traversal/

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var postorderTraversal = function(root) {
    return root ? [
        // 后序遍历：左右中
        ...postorderTraversal(root.left), // 左
        ...postorderTraversal(root.right), // 右
        root.val, // 中
    ] : [];
};
```

### 94. Binary Tree Inorder Traversal

https://leetcode.com/problems/binary-tree-inorder-traversal/description/

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var inorderTraversal = function(root) {
    return root ? [
        // 中序遍历
        ...inorderTraversal(root.left), // 递归左子树
        root.val, // 中
        ...inorderTraversal(root.right) // 递归右子树
    ] : [];
};
```


