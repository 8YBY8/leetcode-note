# 回溯算法 part01

## 理论基础 


文章链接：https://programmercarl.com/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html  

视频讲解：https://www.bilibili.com/video/BV1cy4y167mM  

回溯法，一般可以解决如下几种问题：
- 组合问题：N个数里面按一定规则找出k个数的集合
- 切割问题：一个字符串按一定规则有几种切割方式
- 子集问题：一个N个数的集合里有多少符合条件的子集
- 排列问题：N个数按一定规则全排列，有几种排列方式
- 棋盘问题：N皇后，解数独等等

组合是不强调元素顺序的，排列是强调元素顺序

回溯法解决的都是在集合中递归查找子集，集合的大小就构成了树的宽度，递归的深度就构成了树的深度

回溯三部曲：
1. 回溯函数模板返回值以及参数 回溯函数伪代码：`void backtracking(参数)`
2. 回溯函数终止条件 回溯函数终止条件伪代码:
    ```
    if (终止条件) {
        存放结果;
        return;
    }
    ```
3. 回溯搜索的遍历过程 <img width="1558" height="736" alt="image" src="https://github.com/user-attachments/assets/044a58d0-72e2-4f14-9b2d-b1ff77cf4477" /> for循环就是遍历集合区间，可以理解一个节点有多少个孩子，这个for循环就执行多少次。回溯函数遍历过程伪代码:
   ```cpp
   for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    } 
    ```

回溯算法模板框架:
```cpp
void backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }

    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```

## 77. Combinations

https://leetcode.com/problems/combinations/

<img width="1444" height="614" alt="image" src="https://github.com/user-attachments/assets/4a63382f-c99d-40be-871a-8df4e5248f75" />


回溯法三部曲(思路):
1. 递归函数的返回值以及参数: 在这里要定义两个全局变量，一个用来存放符合条件单一结果，一个用来存放符合条件结果的集合。
2. 回溯函数终止条件：path这个数组的大小如果达到k，说明我们找到了一个子集大小为k的组合了
3. 单层搜索的过程：回溯法的搜索过程就是一个树型结构的遍历过程，在如下图中，可以看出for循环用来横向遍历，递归的过程是纵向遍历。

startIndex 就是防止出现重复的组合
```javascript
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
var combine = function (n, k) {
    // 回溯法
    let result = [], // 存放符合条件结果的集合
        path = []; // 用来存放符合条件结果
    let backtracking = (_n, _k, startIndex) => {
        // 终止条件
        if (path.length === _k) {
            result.push(path.slice());
            return;
        }
        // 循环本层集合元素
        for (let i = startIndex; i <= _n; i++) {
            path.push(i); // 处理节点
            //   递归
            backtracking(_n, _k, i + 1);
            //   回溯操作
            path.pop();
        }
    };
    backtracking(n, k, 1);
    return result;
};
```

剪枝优化
<img width="1588" height="1054" alt="image" src="https://github.com/user-attachments/assets/c6eb31f2-cb3f-4947-8491-195d9c48073d" />
如果for循环选择的起始位置之后的元素个数 已经不足 我们需要的元素个数了，那么就没有必要搜索了

```javascript
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
var combine = function (n, k) {
    // 回溯法
    let result = [], // 存放符合条件结果的集合
        path = []; // 用来存放符合条件结果
    let backtracking = (_n, _k, startIndex) => {
        // 终止条件
        if (path.length === _k) {
            result.push(path.slice());
            return;
        }
        // 循环本层集合元素
        for (let i = startIndex; i <= _n - (_k - path.length) + 1; i++) {
            path.push(i); // 处理节点
            //   递归
            backtracking(_n, _k, i + 1);
            //   回溯操作
            path.pop();
        }
    };
    backtracking(n, k, 1);
    return result;
};
```
