[二叉树 part01](https://github.com/8YBY8/leetcode-note/blob/main/binarytree.md#%E4%BA%8C%E5%8F%89%E6%A0%91-part01)

[二叉树 part02](https://github.com/8YBY8/leetcode-note/blob/main/binarytree.md#%E4%BA%8C%E5%8F%89%E6%A0%91-part02)

[二叉树 part03](https://github.com/8YBY8/leetcode-note/blob/main/binarytree.md#%E4%BA%8C%E5%8F%89%E6%A0%91-part03)

[二叉树 part04](https://github.com/8YBY8/leetcode-note/blob/main/binarytree.md#%E4%BA%8C%E5%8F%89%E6%A0%91-part04)

[二叉树 part05](https://github.com/8YBY8/leetcode-note/blob/main/binarytree.md#%E4%BA%8C%E5%8F%89%E6%A0%91-part05)

# 二叉树 part01

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

## 144. Binary Tree Preorder Traversal

https://leetcode.com/problems/binary-tree-preorder-traversal/

Method 1: 递归遍历1

文章链接：https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%80%92%E5%BD%92%E9%81%8D%E5%8E%86.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC

视频链接：https://www.bilibili.com/video/BV1Wh411S7xt

递归算法的三个要素:
1. 确定递归函数的参数和返回值
2. 确定终止条件
3. 确定单层递归的逻辑

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

Method 2: 递归遍历2

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

Method 3: 迭代遍历

文章链接：https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E8%BF%AD%E4%BB%A3%E9%81%8D%E5%8E%86.html

视频链接：https://www.bilibili.com/video/BV15f4y1W7i2

前序遍历是中左右，每次先处理的是中间节点，那么先将根节点放入栈中，然后将右孩子加入栈，再加入左孩子。

![Binary Tree Preorder Traversal](https://file1.kamacoder.com/i/algo/%E4%BA%8C%E5%8F%89%E6%A0%91%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%EF%BC%88%E8%BF%AD%E4%BB%A3%E6%B3%95%EF%BC%89.gif)

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
    // 入栈 右 -> 左
    // 出栈 中 -> 左 -> 右
    let res = []
    if(!root) return res;
    const stack = [root];
    let cur = null;
    while(stack.length) {
        cur = stack.pop(); // 中
        res.push(cur.val);
        if (cur.right) stack.push(cur.right); // 右
        if (cur.left) stack.push(cur.left); // 左
    }
    return res;
};
```

Method 4: 统一迭代法不推荐因为并不好理解，而且想在面试直接写出来还有难度的

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
    // 前序遍历：中左右
    // 压栈顺序：右左中
    let res = []
    const stack = [];
    if (root) stack.push(root);
    while(stack.length) {
        const node = stack.pop();
        if(!node) {
            res.push(stack.pop().val);
            continue;
        }
        if (node.right) stack.push(node.right); // 右
        if (node.left) stack.push(node.left); // 左
        stack.push(node); // 中
        stack.push(null);
    };
    return res;
};
```

## 145. Binary Tree Postorder Traversal

https://leetcode.com/problems/binary-tree-postorder-traversal/

Method 1: 递归遍历

文章链接：https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%80%92%E5%BD%92%E9%81%8D%E5%8E%86.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC

视频链接：https://www.bilibili.com/video/BV1Wh411S7xt

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

Method 2: 迭代遍历

文章链接：https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E8%BF%AD%E4%BB%A3%E9%81%8D%E5%8E%86.html

视频链接：https://www.bilibili.com/video/BV15f4y1W7i2

<img width="1128" height="262" alt="image" src="https://github.com/user-attachments/assets/8500592b-c129-4b18-a702-5bca4f03b89e" />

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
    // 入栈 左 -> 右
    // 出栈 中 -> 右 -> 左 结果翻转
    let res = [];
    if(!root) return res;
    let st = [root];
    let cur = null
    while(st.length > 0) {
        cur = st.pop(); // 中
        res.push(cur.val);
        if(cur.left) st.push(cur.left); // 左
        if(cur.right) st.push(cur.right); // 右
    }
    return res.reverse();
};
```

Method 3: 统一迭代法

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
    // 后续遍历：左右中
    // 压栈顺序：中右左
    let res = [];
    const stack = [];
    if (root) stack.push(root);
    while(stack.length) {
        const node = stack.pop();
        if(!node) {
            res.push(stack.pop().val);
            continue;
        }
        stack.push(node); // 中
        stack.push(null);
        if (node.right) stack.push(node.right); // 右
        if (node.left) stack.push(node.left); // 左
    };
    return res;
};
```

## 94. Binary Tree Inorder Traversal

https://leetcode.com/problems/binary-tree-inorder-traversal/description/

Method 1: 递归遍历

文章链接：https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%80%92%E5%BD%92%E9%81%8D%E5%8E%86.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC

视频链接：https://www.bilibili.com/video/BV1Wh411S7xt

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

Method 2: 迭代遍历

文章链接：https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E8%BF%AD%E4%BB%A3%E9%81%8D%E5%8E%86.html

视频链接：https://www.bilibili.com/video/BV1Zf4y1a77g

前序和中序的迭代遍历是完全两种代码风格，并不像递归写法那样代码稍做调整，就可以实现前后中序。这是因为前序遍历中访问节点（遍历节点）和处理节点（将元素放进result数组中）可以同步处理，但是中序就无法做到同步

![Binary Tree Inorder Traversal](https://file1.kamacoder.com/i/algo/%E4%BA%8C%E5%8F%89%E6%A0%91%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86%EF%BC%88%E8%BF%AD%E4%BB%A3%E6%B3%95%EF%BC%89.gif)

```javascipt
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
    let res = [];
    const stack = [];
    let cur = root;
    while(stack.length || cur) {
        if(cur) { // 指针来访问节点，访问到最底层
            stack.push(cur); // 将访问的节点放进栈
            // 左
            cur = cur.left;
        } else {
            // --> 弹出 中 
            cur = stack.pop();
            res.push(cur.val); 
            // 右
            cur = cur.right;
        }
    };
    return res;
};
```

Method 3: 统一迭代法

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
    //  中序遍历：左中右
    //  压栈顺序：右中左
    let res = [];
    const stack = [];
    if (root) stack.push(root);
    while(stack.length) {
        const node = stack.pop();
        if(!node) {
            res.push(stack.pop().val);
            continue;
        }
        if (node.right) stack.push(node.right); // 右
        stack.push(node); // 中
        stack.push(null);
        if (node.left) stack.push(node.left); // 左
    };
    return res;
};
```

<img width="1012" height="755" alt="image" src="https://github.com/user-attachments/assets/4405347d-f382-4c8d-bd0c-561c309174ba" />


## 层序遍历 (10道题)

二叉树的层序遍历，就是图论中的广度优先搜索在二叉树中的应用，需要借助队列来实现

文章链接：https://programmercarl.com/0102.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

### 102. Binary Tree Level Order Traversal

https://leetcode.com/problems/binary-tree-level-order-traversal/



视频链接：https://www.bilibili.com/video/BV1GY4y1u7b2

![Binary Tree Level Order Traversal](https://file1.kamacoder.com/i/algo/102%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86.gif)

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
 * @return {number[][]}
 */
var levelOrder = function(root) {
    let res = [], queue = [];
    queue.push(root);
    if(root === null) {
        return res;
    }
    while(queue.length !== 0) {
        // 记录当前层级节点数
        let length = queue.length;
        //存放每一层的节点
        let curLevel = [];
        for(let i = 0;i < length; i++) {
            let node = queue.shift();
            curLevel.push(node.val);
            // 存放当前层下一层的节点
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
        //把每一层的结果放到结果数组
        res.push(curLevel);
    }
    return res;
};
```

### 107. Binary Tree Level Order Traversal II

https://leetcode.com/problems/binary-tree-level-order-traversal-ii/

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
 * @return {number[][]}
 */
var levelOrderBottom = function (root) {
    let res = [], queue = [];
    queue.push(root);
    while (queue.length && root !== null) {
        // 存放当前层级节点数组
        let curLevel = [];
        // 计算当前层级节点数量
        let length = queue.length;
        while (length--) {
            let node = queue.shift();
            // 把当前层节点存入curLevel数组
            curLevel.push(node.val);
            // 把下一层级的左右节点存入queue队列
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
        // 从数组前头插入值，避免最后反转数组，减少运算时间
        res.unshift(curLevel);
    }
    return res;
};
```

### 199. Binary Tree Right Side View

https://leetcode.com/problems/binary-tree-right-side-view/

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
var rightSideView = function(root) {
    //二叉树右视图 只需要把每一层最后一个节点存储到res数组
    let res = [], queue = [];
    queue.push(root);

    while(queue.length && root!==null) {
        // 记录当前层级节点个数
        let length = queue.length;
        while(length--) {
            let node = queue.shift();
            // length长度为0的时候表明到了层级最后一个节点
            if(!length) {
                res.push(node.val);
            }
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
    }

    return res;
};
```

### 637. Average of Levels in Binary Tree

https://leetcode.com/problems/average-of-levels-in-binary-tree/

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
var averageOfLevels = function (root) {
    let res = [], queue = [];
    queue.push(root);
    while (queue.length) {
        // 每一层节点个数;
        let lengthLevel = queue.length,
            len = queue.length,
            //   sum记录每一层的和;
            sum = 0;
        while (lengthLevel--) {
            const node = queue.shift();
            sum += node.val;
            //   队列存放下一层节点
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
        // 求平均值
        res.push(sum / len);
    }
    return res;
};
```

### 429. N-ary Tree Level Order Traversal

https://leetcode.com/problems/n-ary-tree-level-order-traversal/

```javascript
/**
 * // Definition for a _Node.
 * function _Node(val,children) {
 *    this.val = val;
 *    this.children = children;
 * };
 */

/**
 * @param {_Node|null} root
 * @return {number[][]}
 */
var levelOrder = function (root) {
    //每一层可能有2个以上,所以不再使用node.left node.right
    let res = [], queue = [];
    queue.push(root);

    while (queue.length && root !== null) {
        //记录每一层节点个数还是和二叉树一致
        let length = queue.length;
        //存放每层节点 也和二叉树一致
        let curLevel = [];
        while (length--) {
            let node = queue.shift();
            curLevel.push(node.val);

            //这里不再是 ndoe.left node.right 而是循坏node.children
            for (let item of node.children) {
                item && queue.push(item);
            }
        }
        res.push(curLevel);
    }

    return res;
};
```

### 515. Find Largest Value in Each Tree Row

https://leetcode.com/problems/find-largest-value-in-each-tree-row/

```javascript/**
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
var largestValues = function (root) {
    let res = [],
        queue = [];
    queue.push(root);
    if (root === null) {
        return res;
    }
    while (queue.length) {
        let lengthLevel = queue.length,
            // 初始值设为负无穷大
            max = -Infinity;
        while (lengthLevel--) {
            const node = queue.shift();
            //   在当前层中找到最大值
            max = Math.max(max, node.val);
            // 找到下一层的节点
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
        res.push(max);
    }
    return res;
};
```

### 116. Populating Next Right Pointers in Each Node

https://leetcode.com/problems/populating-next-right-pointers-in-each-node/

```javascript
/**
 * // Definition for a _Node.
 * function _Node(val, left, right, next) {
 *    this.val = val === undefined ? null : val;
 *    this.left = left === undefined ? null : left;
 *    this.right = right === undefined ? null : right;
 *    this.next = next === undefined ? null : next;
 * };
 */

/**
 * @param {_Node} root
 * @return {_Node}
 */
var connect = function(root) {
    if (!root) return root
    let queue = [root]
    while (queue.length) {
        let n = queue.length;
        for (let i = 0; i < n; i++) {
            let node = queue.shift();
            if (i < n-1) {
                node.next = queue[0];
            }
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
    }
    return root;
};
```

### 117. Populating Next Right Pointers in Each Node II

https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/

```javascript
/**
 * // Definition for a _Node.
 * function _Node(val, left, right, next) {
 *    this.val = val === undefined ? null : val;
 *    this.left = left === undefined ? null : left;
 *    this.right = right === undefined ? null : right;
 *    this.next = next === undefined ? null : next;
 * };
 */

/**
 * @param {_Node} root
 * @return {_Node}
 */
var connect = function (root) {
    if (root === null) {
        return null;
    }
    let queue = [root];
    while (queue.length > 0) {
        let n = queue.length;
        for (let i = 0; i < n; i++) {
            let node = queue.shift();
            if (i < n - 1) node.next = queue[0];
            if (node.left != null) queue.push(node.left);
            if (node.right != null) queue.push(node.right);
        }
    }
    return root;
};
```

### 104. Maximum Depth of Binary Tree

https://leetcode.com/problems/maximum-depth-of-binary-tree/

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
 * @return {number}
 */
var maxDepth = function (root) {
    // 二叉树的 最大深度 是指从根节点到最远叶子节点的最长路径上的节点数。
    let max = 0,
        queue = [root];
    if (root === null) {
        return max;
    }
    while (queue.length) {
        max++;
        let length = queue.length;
        while (length--) {
            let node = queue.shift();
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
    }
    return max;
};
```<img width="1012" height="755" alt="image" src="https://github.com/user-attachments/assets/200fb26a-0214-4d15-b572-00dffd11cd9e" />


### 111. Minimum Depth of Binary Tree

https://leetcode.com/problems/minimum-depth-of-binary-tree/

需要注意的是，只有当左右孩子都为空的时候，才说明遍历的最低点了。如果其中一个孩子为空则不是最低点

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
 * @return {number}
 */
var minDepth = function (root) {
    if (root === null) return 0;
    let queue = [root];
    let depth = 0;
    while (queue.length) {
        let n = queue.length;
        depth++;
        for (let i = 0; i < n; i++) {
            let node = queue.shift();
            // 如果左右节点都是null(在遇见的第一个leaf节点上)，则该节点深度最小
            if (node.left === null && node.right === null) {
                return depth;
            }
            node.left && queue.push(node.left);;
            node.right && queue.push(node.right);
        }
    }
    return depth;
};
```

# 二叉树 part02

## 226. Invert Binary Tree

https://leetcode.com/problems/invert-binary-tree/

文章链接：

视频链接：

针对二叉树的问题，解题之前一定要想清楚究竟是前中后序遍历，还是层序遍历。

Method 1: 递归前序遍历
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
 * @return {TreeNode}
 */
var invertTree = function(root) {
    // 终止条件
    if (!root) {
        return null;
    }
    // 交换左右节点 前序遍历
    const rightNode = root.right; // 中
    root.right = invertTree(root.left); // 左
    root.left = invertTree(rightNode); // 右
    return root;
};
```

Method 2: 迭代前序遍历

```javascript
var invertTree = function(root) {
    //我们先定义节点交换函数
    const invertNode = function(root, left, right) {
        let temp = left;
        left = right;
        right = temp;
        root.left = left;
        root.right = right;
    }
    //使用迭代方法的前序遍历 
    let stack = [];
    if(root === null) {
        return root;
    }
    stack.push(root);
    while(stack.length) {
        let node = stack.pop();
        if(node !== null) {
            //前序遍历顺序中左右  入栈顺序是前序遍历的倒序右左中
            node.right && stack.push(node.right);
            node.left && stack.push(node.left);
            stack.push(node);
            stack.push(null);
        } else {
            node = stack.pop();
            //节点处理逻辑
            invertNode(node, node.left, node.right);
        }
    }
    return root;
};
```

## 101. Symmetric Tree

https://leetcode.com/problems/symmetric-tree/

文章链接：https://programmercarl.com/0101.%E5%AF%B9%E7%A7%B0%E4%BA%8C%E5%8F%89%E6%A0%91.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1ue4y1Y7Mf

<img width="1074" height="774" alt="image" src="https://github.com/user-attachments/assets/c10fd8b3-502a-4336-95ab-39f5cd41440e" />


Method 1: 递归
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
 * @return {boolean}
 */
var isSymmetric = function (root) {
    // 使用递归遍历左右子树 递归三部曲
    // 1. 确定递归的参数 root.left root.right和返回值true false 
    const compareNode = function (left, right) {
        // 2. 确定终止条件 空的情况
        if (left === null && right !== null || left !== null && right === null) {  // 首先排除空节点的情况
            return false;
        } else if (left === null && right === null) {
            return true;
        } else if (left.val !== right.val) { // 排除了空节点，再排除数值不相同的情况
            return false;
        }
        // 3. 确定单层递归逻辑
        let outSide = compareNode(left.left, right.right); // 左子树：左、 右子树：右
        let inSide = compareNode(left.right, right.left);  // 左子树：右、 右子树：左
        return outSide && inSide;                          // 左子树：中、 右子树：中（逻辑处理）
    }
    if (root === null) {
        return true;
    }
    return compareNode(root.left, root.right);
};
```

Method 2:迭代
```javascript
var isSymmetric = function(root) {
  // 迭代方法判断是否是对称二叉树
  // 首先判断root是否为空
  if(root === null) {
      return true;
  }
  let queue = [];
  queue.push(root.left);
  queue.push(root.right);
  while(queue.length) {
      let leftNode = queue.shift();    //左节点
      let rightNode = queue.shift();   //右节点
      if(leftNode === null && rightNode === null) {
          continue;
      }
      if(leftNode === null || rightNode === null || leftNode.val !== rightNode.val) {
          return false;
      }
      queue.push(leftNode.left);     //左节点左孩子入队
      queue.push(rightNode.right);   //右节点右孩子入队
      queue.push(leftNode.right);    //左节点右孩子入队
      queue.push(rightNode.left);    //右节点左孩子入队
  }
  
  return true;
};
```

## 104. Maximum Depth of Binary Tree

https://leetcode.com/problems/maximum-depth-of-binary-tree/description/

文章链接：https://programmercarl.com/0104.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1Gd4y1V75u

二叉树节点的深度：指从根节点到该节点的最长简单路径边的条数或者节点数（取决于深度从0开始还是从1开始）
二叉树节点的高度：指从该节点到叶子节点的最长简单路径边的条数或者节点数（取决于高度从0开始还是从1开始）

Method 1: 递归Recursion
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
 * @return {number}
 */
var maxDepth = function(root) {
    if (root === null) return 0;
    let leftDepth = maxDepth(root.left); // 左
    let rightDepth = maxDepth(root.right); // 右
    let depth = 1 + Math.max(leftDepth, rightDepth); // 中
    return depth
};
```

Method 2: 迭代Iteration
https://github.com/8YBY8/leetcode-note/blob/main/binarytree.md#104-maximum-depth-of-binary-tree


## 559. Maximum Depth of N-ary Tree

https://leetcode.com/problems/maximum-depth-of-n-ary-tree/description/

```javascript
/**
 * // Definition for a _Node.
 * function _Node(val,children) {
 *    this.val = val === undefined ? null : val;
 *    this.children = children === undefined ? null : children;
 * };
 */

/**
 * @param {_Node|null} root
 * @return {number}
 */
var maxDepth = function(root) {
    if(!root) return 0
    let depth = 0
    for(let node of root.children) {
        depth = Math.max(depth, maxDepth(node))
    }
    return depth + 1
};
```

## 111. Minimum Depth of Binary Tree

https://leetcode.com/problems/minimum-depth-of-binary-tree/

文章链接：https://programmercarl.com/0111.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%B0%8F%E6%B7%B1%E5%BA%A6.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1QD4y1B7e2

<img width="958" height="748" alt="image" src="https://github.com/user-attachments/assets/1a5e29ca-6d0b-408f-8ae4-6eebd142e8e4" />

求二叉树的最小深度和求二叉树的最大深度的差别主要在于处理左右孩子不为空的逻辑: 如果左子树为空，右子树不为空，说明最小深度是 1 + 右子树的深度。反之，右子树为空，左子树不为空，最小深度是 1 + 左子树的深度。 最后如果左右子树都不为空，返回左右子树深度最小值 + 1 。

Method 1: 递归
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
 * @return {number}
 */
var minDepth = function(root) {
    if(!root) return 0;
    // 到叶子节点 返回 1
    if(!root.left && !root.right) return 1;
    let leftDepth = minDepth(root.left)
    let rightDepth = minDepth(root.right)

    // 当一个左子树为空，右不为空，这时并不是最低点
    if (root.left === null && root.right !== null) return 1 + rightDepth
    // 当一个右子树为空，左不为空，这时并不是最低点
    if (root.left !== null && root.right === null) return 1 + leftDepth
    return 1 + Math.min(leftDepth, rightDepth)
};
```

Method 2: 迭代
https://github.com/8YBY8/leetcode-note/edit/main/binarytree.md#111-minimum-depth-of-binary-tree

# 二叉树 part03

在递归法，求二叉树的高度用后序遍历，深度用前序遍历。

<img width="700" height="720" alt="image" src="https://github.com/user-attachments/assets/8c18f286-67d7-49ac-8be0-14c4747e551e" />

## 110. Balanced Binary Tree

https://leetcode.com/problems/balanced-binary-tree/

文章链接：https://programmercarl.com/0110.%E5%B9%B3%E8%A1%A1%E4%BA%8C%E5%8F%89%E6%A0%91.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1Ug411S7my

Method 1: 递归
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
 * @return {boolean}
 */
var isBalanced = function(root) {
    // 用递归三部曲 + 后序遍历 左右中 当前左子树右子树高度相差大于1就返回-1
    // 1. 确定递归函数参数以及返回值
    const getDepth = function(node) {
        // 2. 确定递归函数终止条件
        if(node === null) return 0;
        // 3. 确定单层递归逻辑
        let leftDepth = getDepth(node.left); //左子树高度
        // 当判定左子树不为平衡二叉树时,即可直接返回-1
        if(leftDepth === -1) return -1;
        let rightDepth = getDepth(node.right); //右子树高度
        // 当判定右子树不为平衡二叉树时,即可直接返回-1
        if(rightDepth === -1) return -1;
        if(Math.abs(leftDepth - rightDepth) > 1) {
            return -1;
        } else {
            return 1 + Math.max(leftDepth, rightDepth);
        }
    }
    return !(getDepth(root) === -1);
}
```

Method 2: 迭代
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */

var getHeight = function (curNode) {
    let queue = [];
    if (curNode !== null) queue.push(curNode); // 压入当前元素
    let depth = 0, res = 0;
    while (queue.length) {
        let node = queue[queue.length - 1]; // 取出栈顶
        if (node !== null) {
            queue.pop();
            queue.push(node);   // 中
            queue.push(null);
            depth++;
            node.right && queue.push(node.right);   // 右
            node.left && queue.push(node.left);     // 左
        } else {
            queue.pop();
            node = queue[queue.length - 1];
            queue.pop();
            depth--;
        }
        res = res > depth ? res : depth;
    }
    return res;
}
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isBalanced = function (root) {
    if (root === null) return true;
    let queue = [root];
    while (queue.length) {
        let node = queue[queue.length - 1]; // 取出栈顶
        queue.pop();
        if (Math.abs(getHeight(node.left) - getHeight(node.right)) > 1) {
            return false;
        }
        node.right && queue.push(node.right);
        node.left && queue.push(node.left);
    }
    return true;
};
```

## 257. Binary Tree Paths

https://leetcode.com/problems/binary-tree-paths/

文章链接：https://programmercarl.com/0257.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%89%80%E6%9C%89%E8%B7%AF%E5%BE%84.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1ZG411G7Dh

<img width="940" height="820" alt="image" src="https://github.com/user-attachments/assets/07243f30-9335-4483-a2c2-4fd7e9d5bd25" />


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
 * @return {string[]}
 */
var binaryTreePaths = function(root) {
    //递归遍历+递归三部曲
   let res = [];
   //1. 确定递归函数 函数参数
   const getPath = function(node,curPath) {
    //2. 确定终止条件，到叶子节点就终止
       if(node.left === null && node.right === null) {
           curPath += node.val;
           res.push(curPath);
           return;
       }
       //3. 确定单层递归逻辑
       curPath += node.val + '->'; // 中
       node.left && getPath(node.left, curPath); // 左
       node.right && getPath(node.right, curPath); // 右
   }
   getPath(root, '');
   return res;
};
```
迭代法：**回溯隐藏在traversal(cur->left, path + "->", result);中的 path + "->"。 每次函数调用完，path依然是没有加上"->" 的，这就是回溯了**


## 404. Sum of Left Leaves

https://leetcode.com/problems/sum-of-left-leaves/

文章链接：https://programmercarl.com/0404.%E5%B7%A6%E5%8F%B6%E5%AD%90%E4%B9%8B%E5%92%8C.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1GY4y1K7z8

<img width="916" height="748" alt="image" src="https://github.com/user-attachments/assets/0407830b-6a6b-470a-a651-64b4ffdcdc36" />

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
 * @return {number}
 */
var sumOfLeftLeaves = function(root) {
    //采用后序遍历 递归遍历
    // 1. 确定递归函数参数
    const nodesSum = function(node) {
        // 2. 确定终止条件
        if(node === null) {
            return 0;
        }
        let leftValue = nodesSum(node.left);
        let rightValue = nodesSum(node.right);
        // 3. 单层递归逻辑
        let midValue = 0;
        if(node.left && node.left.left === null && node.left.right === null) {
            midValue = node.left.val;
        }
        let sum = midValue + leftValue + rightValue;
        return sum;
    }
    return nodesSum(root);
};
```

## 222. Count Complete Tree Nodes

https://leetcode.com/problems/count-complete-tree-nodes/

文章链接：https://programmercarl.com/0222.%E5%AE%8C%E5%85%A8%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E8%8A%82%E7%82%B9%E4%B8%AA%E6%95%B0.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1eW4y1B7pD

如果是二叉树
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
 * @return {number}
 */
var countNodes = function(root) {
    //递归法计算二叉树节点数
    // 1. 确定递归函数参数
    const getNodeSum = function(node) {
    //2. 确定终止条件
        if(node === null) {
            return 0;
        }
    //3. 确定单层递归逻辑
        let leftNum = getNodeSum(node.left);
        let rightNum = getNodeSum(node.right);
        return leftNum + rightNum + 1;
    }
    return getNodeSum(root);
};
```

如果是完全二叉树
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
 * @return {number}
 */
var countNodes = function(root) {
    //利用完全二叉树的特点
    if(root === null) {
        return 0;
    }
    let left = root.left;
    let right = root.right;
    let leftDepth = 0, rightDepth = 0;
    while(left) {
        left = left.left;
        leftDepth++;
    }
    while(right) {
        right = right.right;
        rightDepth++;
    }
    if(leftDepth == rightDepth) {
        return Math.pow(2, leftDepth+1) - 1;
    }
    return countNodes(root.left) + countNodes(root.right) + 1;
};
```

# 二叉树 part04

## 513. Find Bottom Left Tree Value

https://leetcode.com/problems/find-bottom-left-tree-value/

文章链接：https://programmercarl.com/0513.%E6%89%BE%E6%A0%91%E5%B7%A6%E4%B8%8B%E8%A7%92%E7%9A%84%E5%80%BC.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1424y1Z7pn

Method 1: 迭代（更简单）
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
 * @return {number}
 */
var findBottomLeftValue = function(root) {
    //考虑层序遍历 记录最后一行的第一个节点
    let queue = [];
    if(root === null) { 
        return null;
    }
    queue.push(root);
    let resNode;
    while(queue.length) {
        let length = queue.length;
        for(let i = 0; i < length; i++) {
            let node = queue.shift();
            if(i === 0) { // 记录最后一行的第一个节点
                resNode = node.val;
            }
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
    }
    return resNode;
};
```

Method 2:递归
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
 * @return {number}
 */
var findBottomLeftValue = function (root) {
    //首先考虑递归遍历 前序遍历 找到最大深度的叶子节点即可
    let maxDepth = 0, resNode = null;
    // 1. 确定递归函数的函数参数
    const dfsTree = function (node, curDepth) {
        // 2. 确定递归函数终止条件
        if (node.left === null && node.right === null) {
            if (curDepth > maxDepth) {
                maxDepth = curDepth;
                resNode = node.val;
            }
        }
        if (node.left) {
            curDepth++;
            dfsTree(node.left, curDepth);
            curDepth--;
        };
        if (node.right) {
            curDepth++;
            dfsTree(node.right, curDepth);
            curDepth--;
        };
    }
    dfsTree(root, 1);
    return resNode;
};
```

## 112. Path Sum

https://leetcode.com/problems/path-sum/

递归函数什么时候需要返回值？什么时候不需要返回值？这里总结如下三点：
1. 如果需要搜索整棵二叉树且不用处理递归返回值，递归函数就不要返回值。（这种情况就是本文下半部分介绍的113.路径总和ii）
2. 如果需要搜索整棵二叉树且需要处理递归返回值，递归函数就需要返回值。 （这种情况我们在236. 二叉树的最近公共祖先 (opens new window)中介绍）
3. 如果要搜索其中一条符合条件的路径，那么递归一定需要返回值，因为遇到符合条件的路径了就要及时返回。（112. 路径总和的情况）

**用不用回溯** : 取决于修改后的变量传入下一层函数后 本层函数还需不需要它了  是需要它改变后的值还是原值  一般要原值就回溯  要修改后的值通过定义函数返回值来得到

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
 * @param {number} targetSum
 * @return {boolean}
 */
var hasPathSum = function (root, targetSum) {
    // 递归法
    const traversal = (node, cnt) => {
        // 遇到叶子节点，并且计数为0
        if (cnt === 0 && !node.left && !node.right) return true;
        // 遇到叶子节点而没有找到合适的边(计数不为0)，直接返回
        if (!node.left && !node.right) return false;

        //  左（空节点不遍历）.遇到叶子节点返回true，则直接返回true
        if (node.left && traversal(node.left, cnt - node.left.val)) return true;
        //  右（空节点不遍历）
        if (node.right && traversal(node.right, cnt - node.right.val)) return true;
        return false;
    };
    if (!root) return false;
    return traversal(root, targetSum - root.val);

    // 精简代码:
    // if (!root) return false;
    // if (!root.left && !root.right && targetsum === root.val) return true;
    // return haspathsum(root.left, targetsum - root.val) || haspathsum(root.right, targetsum - root.val);
};
```

## 113. Path Sum II

https://leetcode.com/problems/path-sum-ii/

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
 * @param {number} targetSum
 * @return {number[][]}
 */
var pathSum = function(root, targetSum) {
    // 递归法
  // 要遍历整个树找到所有路径，所以递归函数不需要返回值, 与112不同
  const res = [];
  const travelsal = (node, cnt, path) => {
    // 遇到了叶子节点且找到了和为sum的路径
    if (cnt === 0 && !node.left && !node.right) {
      res.push([...path]); // 不能写res.push(path), 要深拷贝
      return;
    }
    if (!node.left && !node.right) return; // 遇到叶子节点而没有找到合适的边，直接返回
    // 左 （空节点不遍历）
    if (node.left) {
      path.push(node.left.val);
      travelsal(node.left, cnt - node.left.val, path); // 递归
      path.pop(); // 回溯
    }
    // 右 （空节点不遍历）
    if (node.right) {
      path.push(node.right.val);
      travelsal(node.right, cnt - node.right.val, path); // 递归
      path.pop(); // 回溯
    }
    return;
  };
  if (!root) return res;
  travelsal(root, targetSum - root.val, [root.val]); // 把根节点放进路径
  return res;
};
```

## 106. Construct Binary Tree from Inorder and Postorder Traversal

https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/

<img width="1292" height="786" alt="image" src="https://github.com/user-attachments/assets/f10c3e05-84f6-4dac-8bc1-6ffce16a405a" />

思路：
1. 如果数组大小为零的话，说明是空节点了。
2. 如果不为空，那么取后序数组最后一个元素作为节点元素。
3. 找到后序数组最后一个元素在中序数组的位置，作为切割点
4. 切割中序数组，切成中序左数组和中序右数组 （顺序别搞反了，一定是先切中序数组）
5. 切割后序数组，切成后序左数组和后序右数组
6. 递归处理左区间和右区间

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
 * @param {number[]} inorder
 * @param {number[]} postorder
 * @return {TreeNode}
 */
var buildTree = function(inorder, postorder) {
    if (!inorder.length) return null;
    const rootVal = postorder.pop(); // 从后序遍历的数组中获取中间节点的值， 即数组最后一个值
    let rootIndex = inorder.indexOf(rootVal); // 获取中间节点在中序遍历中的下标
    const root = new TreeNode(rootVal); // 创建中间节点

    // 切割中序数组
    // 左闭右开区间：[0, delimiterIndex)
    let leftInorder = inorder.slice(0, rootIndex);
    // [rootIndex + 1, end)
    let rightInorder = inorder.slice(rootIndex + 1);

    // 切割后序数组
    // 依然左闭右开，注意这里使用了左中序数组大小作为切割点
    // [0, leftInorder.size)
    let leftPostorder = postorder.slice(0, rootIndex);
    // [leftInorder.size(), end)
    let rightPostorder = postorder.slice(rootIndex);
    root.left = buildTree(leftInorder, leftPostorder); // 创建左节点
    root.right = buildTree(rightInorder, rightPostorder); // 创建右节点
    return root;
};
```

## 105. Construct Binary Tree from Preorder and Inorder Traversal

https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

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
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */
var buildTree = function(preorder, inorder) {
    if (!preorder.length) return null;
    const rootVal = preorder.shift(); // 从前序遍历的数组中获取中间节点的值， 即数组第一个值
    let rootIndex = inorder.indexOf(rootVal); // 获取中间节点在中序遍历中的下标
    const root = new TreeNode(rootVal); // 创建中间节点

    // 切割中序数组
    // 左闭右开区间：[0, rootIndex)
    let leftInorder = inorder.slice(0, rootIndex);
    // [rootIndex + 1, end)
    let rightInorder = inorder.slice(rootIndex + 1);

    // 切割前序数组
    // 依然左闭右开
    let leftPreorder = preorder.slice(0, rootIndex);
    let rightPreorder = preorder.slice(rootIndex);
    
    root.left = buildTree(leftPreorder, leftInorder); // 创建左节点
    root.right = buildTree(rightPreorder, rightInorder); // 创建右节点

    return root;
};
```

前序和中序可以唯一确定一棵二叉树。

后序和中序可以唯一确定一棵二叉树。

前序和后序不能唯一确定一棵二叉树！，因为没有中序遍历无法确定左右部分，也就是无法分割。

# 二叉树 part05

## 654. Maximum Binary Tree

https://leetcode.com/problems/maximum-binary-tree/

文章讲解：https://programmercarl.com/0654.%E6%9C%80%E5%A4%A7%E4%BA%8C%E5%8F%89%E6%A0%91.html  

视频讲解：https://www.bilibili.com/video/BV1MG411G7ox  

![654. Maximum Binary Tree](https://file1.kamacoder.com/i/algo/654.%E6%9C%80%E5%A4%A7%E4%BA%8C%E5%8F%89%E6%A0%91.gif)

思路：
1. 找到数组中最大的值和对应的下标
2. 最大值所在的下标左区间 构造左子树
3. 最大值所在的下标右区间 构造右子树

**什么时候递归函数前面加if，什么时候不加if**：一般情况来说：如果让空节点（空指针）进入递归，就不加if，如果不让空节点进入递归，就加if限制一下， 终止条件也会相应的调整

注意类似用数组构造二叉树的题目，每次分隔尽量不要定义新的数组，而是通过下标索引直接在原数组上操作，这样可以节约时间和空间上的开销

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
 * @param {number[]} nums
 * @return {TreeNode}
 */
var constructMaximumBinaryTree = function(nums) {
    const BuildTree = (arr, left, right) => {
        if (left > right)
            return null;
        let maxValue = -1;
        let maxIndex = -1;
        // 找到数组中最大的值和对应的下标
        for (let i = left; i <= right; ++i) {
            if (arr[i] > maxValue) {
                maxValue = arr[i];
                maxIndex = i;
            }
        }
        let root = new TreeNode(maxValue);
        root.left = BuildTree(arr, left, maxIndex - 1); // 最大值所在的下标左区间 构造左子树 左闭右开：[left, maxValueIndex)
        root.right = BuildTree(arr, maxIndex + 1, right); // 最大值所在的下标右区间 构造右子树 左闭右开：[maxValueIndex + 1, right)
        return root;
    }
    let root = BuildTree(nums, 0, nums.length - 1);
    return root;
};
```

## 617. Merge Two Binary Trees

https://leetcode.com/problems/merge-two-binary-trees/

文章讲解：https://programmercarl.com/0617.%E5%90%88%E5%B9%B6%E4%BA%8C%E5%8F%89%E6%A0%91.html  

视频讲解：https://www.bilibili.com/video/BV1m14y1Y7JK

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
 * @param {TreeNode} root1
 * @param {TreeNode} root2
 * @return {TreeNode}
 */
var mergeTrees = function(root1, root2) {
    if (!root1) return root2; // 如果root1为空，合并之后就应该是root2
    if (!root2) return root1; // 如果root2为空，合并之后就应该是root1
    // 修改了root1的数值和结构, 比创建一个新的tree省空间
    root1.val += root2.val;                             // 中
    root1.left = mergeTrees(root1.left, root2.left);    // 左
    root1.right = mergeTrees(root1.right, root2.right); // 右
    return root1;
};
```
