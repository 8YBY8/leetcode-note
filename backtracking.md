[回溯算法 part01](https://github.com/8YBY8/leetcode-note/blob/main/backtracking.md#%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95-part01)

[回溯算法 part02](https://github.com/8YBY8/leetcode-note/blob/main/backtracking.md#%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95-part02)

[回溯算法 part03](https://github.com/8YBY8/leetcode-note/blob/main/backtracking.md#%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95-part03)

[回溯算法 part04](https://github.com/8YBY8/leetcode-note/blob/main/backtracking.md#%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95-part04)


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

**i那里的剪枝可以这么理解，假设从i开始取，则从i到n一共有n-i+1个元素，而当前还需要k-path.size()个元素，所以必须满足n-i+1>=k-path.size()，移项就可以得到i<=n+1-(k-path.size())**

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

## 216. Combination Sum III

https://leetcode.com/problems/combination-sum-iii/

文章链接：https://programmercarl.com/0216.%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8CIII.html   

视频讲解：https://www.bilibili.com/video/BV1wg411873x

<img width="2026" height="1046" alt="image" src="https://github.com/user-attachments/assets/e592f65a-59ad-49b0-a1d5-8600dcb1b04a" />

<img width="2018" height="1010" alt="image" src="https://github.com/user-attachments/assets/c4a7c043-57cd-4c0e-9eac-dd17ef5c8dc7" />
已选元素总和如果已经大于n（图中数值为4）了，那么往后遍历就没有意义了，直接剪掉。

**i那里的剪枝可以这么理解，假设从i开始取，则从i到n一共有n-i+1个元素，而当前还需要k-path.size()个元素，所以必须满足n-i+1>=k-path.size()，移项就可以得到i<=n+1-(k-path.size())**

```javascript
/**
 * @param {number} k
 * @param {number} n
 * @return {number[][]}
 */
var combinationSum3 = function (k, n) {
    // 回溯法
    let result = [], // 存放结果集
        path = []; // 符合条件的结果
    const backtracking = (_k, targetSum, sum, startIndex) => {
        if (sum > targetSum) { // 剪枝操作
            return;
        }
        // 终止条件
        if (path.length === _k) {
            if (sum === targetSum) {
                result.push(path.slice());
            }
            // 如果总和不相等，就直接返回
            return;
        }

        // 循环当前节点，因为只使用数字1到9，所以最大是9
        for (let i = startIndex; i <= 9 - (_k - path.length) + 1; i++) {
            path.push(i);
            sum += i;
            // 回调函数
            backtracking(_k, targetSum, sum, i + 1);
            // 回溯
            sum -= i;
            path.pop();
        }
    };
    backtracking(k, n, 0, 1);
    return result;
};
```

## 17. Letter Combinations of a Phone Number

https://leetcode.com/problems/letter-combinations-of-a-phone-number/

<img width="1486" height="728" alt="image" src="https://github.com/user-attachments/assets/7f1bf204-2b1e-4d62-a3dd-a2e3e63c8c63" />

```javascript
/**
 * @param {string} digits
 * @return {string[]}
 */
var letterCombinations = function (digits) {
    const k = digits.length;
    const map = ["", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"];
    if (!k) return [];
    if (k === 1) return map[digits].split("");

    const res = [], path = [];
    backtracking(digits, k, 0);
    return res;

    function backtracking(n, k, a) {
        if (path.length === k) {
            res.push(path.join(""));
            return;
        }
        for (const v of map[n[a]]) { // 取数字对应的字符集
            path.push(v); // 处理
            backtracking(n, k, a + 1); // 递归，注意a+1，一下层要处理下一个数字了
            path.pop(); // 回溯
        }
    }
};
```

# 回溯算法 part02

## 39. Combination Sum

https://leetcode.com/problems/combination-sum/

<img width="1630" height="896" alt="image" src="https://github.com/user-attachments/assets/9438855e-12fb-48bd-b051-580fb73382b8" />


```javascript
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function (candidates, target) {
    const res = [], path = [];
    candidates.sort((a, b) => a - b); // 需要排序
    
    function backtracking(j, sum) {
        if (sum === target) {
            res.push(Array.from(path));
            return;
        }
        for (let i = j; i < candidates.length; i++) {
            const n = candidates[i];
            if (n > target - sum) break; // 如果 sum + candidates[i] > target 就终止遍历
            path.push(n);
            sum += n;
            backtracking(i, sum); // 不用i+1了，表示可以重复读取当前的数
            path.pop();
            sum -= n;
        }
    }
    
    backtracking(0, 0);
    return res;
};
```

## 40. Combination Sum II

https://leetcode.com/problems/combination-sum-ii/

```javascript
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum2 = function(candidates, target) {
    const res = []; path = [], len = candidates.length;
    candidates.sort((a,b)=>a-b);
    backtracking(0, 0);
    return res;
    function backtracking(sum, i) {
        if (sum === target) {
            res.push(Array.from(path));
            return;
        }
        for(let j = i; j < len; j++) {
            const n = candidates[j];
            // 要对同一树层使用过的元素进行跳过
            if(j > i && candidates[j] === candidates[j-1]){
              //若当前元素和前一个元素相等
              //则本次循环结束，防止出现重复组合
              continue;
            }
            //如果当前元素值大于目标值-总和的值
            //由于数组已排序，那么该元素之后的元素必定不满足条件
            //直接终止当前层的递归
            if(n > target - sum) break;
            path.push(n);
            sum += n;
            backtracking(sum, j + 1);
            path.pop();
            sum -= n;
        }
    }
};
```

## 131. Palindrome Partitioning

https://leetcode.com/problems/palindrome-partitioning/

<img width="1456" height="840" alt="image" src="https://github.com/user-attachments/assets/e9e14a78-5a10-401e-89dd-8d9e24c778cd" />


```javascript
/**
 * @param {string} s
 * @return {string[][]}
 */
var partition = function (s) {
    const res = [], path = [], len = s.length;
    backtracking(0);
    return res;
    function backtracking(startIndex) {
        // 如果起始位置已经大于s的大小，说明已经找到了一组分割方案了
        if (startIndex >= len) {
            res.push(Array.from(path));
            return;
        }
        for (let i = startIndex; i < len; i++) {
            if (!isPalindrome(s, startIndex, i)) continue; // 不是回文，跳过
            // 是回文子串
            // 获取[startIndex,i]在s中的子串
            path.push(s.slice(startIndex, i + 1)); 
            backtracking(i + 1);
            path.pop();
        }
    }
};

const isPalindrome = (s, l, r) => {
    for (let i = l, j = r; i < j; i++, j--) {
        if (s[i] !== s[j]) return false;
    }
    return true;
}
```

# 回溯算法 part03

## 93. Restore IP Addresses

https://leetcode.com/problems/restore-ip-addresses/

<img width="1594" height="734" alt="image" src="https://github.com/user-attachments/assets/0b99aabc-4967-4eb2-b528-894803c3a4b7" />

```javascript
/**
 * @param {string} s
 * @return {string[]}
 */
var restoreIpAddresses = function (s) {
    const res = [], // 记录结果
        path = [];
    backtracking(0);
    return res;
    function backtracking(startIndex) {
        const len = path.length;
        if (len > 4) return;
        // 已切成4段并且已经包括最后一个数，在每个段之间插入"." 加到res里
        if (len === 4 && startIndex === s.length) {
            res.push(path.join("."));
            return;
        }
        for (let j = startIndex; j < s.length; j++) {
            const str = s.slice(startIndex, j + 1);
            // 如果大于255了不合法
            if (str.length > 3 || +str > 255) break; // +str converts the string to a number
            // 0开头的数字不合法
            if (str.length > 1 && str[0] === "0") break;
            path.push(str);
            backtracking(j + 1);
            path.pop(); // 回溯
        }
    }
};
```

## 78. Subsets

https://leetcode.com/problems/subsets/

<img width="1546" height="902" alt="image" src="https://github.com/user-attachments/assets/1d4945dc-15b5-4d53-acfd-c2c5ffb4d2cf" />

**子集是收集树形结构中树的所有节点的结果。而组合问题、分割问题是收集树形结构中叶子节点的结果。**

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsets = function (nums) {
    let result = [];
    let path = [];
    function backtracking(startIndex) {
        result.push(path.slice()); // 收集子集，要放在终止添加的上面，否则会漏掉自己
        if (startIndex >= nums.length) { // 终止条件可以不加
            return;
        }
        for (let i = startIndex; i < nums.length; i++) {
            path.push(nums[i]);
            backtracking(i + 1);
            path.pop();
        };
    }
    backtracking(0);
    return result;
};
```

## 90. Subsets II

https://leetcode.com/problems/subsets-ii/

本题就是40.组合总和II 和 78.子集的结合

<img width="1752" height="1036" alt="image" src="https://github.com/user-attachments/assets/ddb05da3-5d77-4b6f-8b28-1da149007778" />

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsetsWithDup = function (nums) {
    let res = [],
        path = [];
    nums = nums.sort(); // 去重需要排序
    function backtracking(startIndex) {
        res.push(path.slice());
        if (startIndex > nums.length - 1) {
            return
        }
        for (let i = startIndex; i < nums.length; i++) {
            // 我们要对同一树层使用过的元素进行跳过
            if (i > startIndex && nums[i] === nums[i - 1]) {
                //若当前元素和前一个元素相等
                //则本次循环结束，防止出现重复组合
                continue;
            }
            path.push(nums[i]);
            backtracking(i + 1);
            path.pop();
        }
    }
    backtracking(0);
    return res;
};
```

# 回溯算法 part04

## 491. Non-decreasing Subsequences

文章链接：https://programmercarl.com/0491.%E9%80%92%E5%A2%9E%E5%AD%90%E5%BA%8F%E5%88%97.html

视频讲解：https://www.bilibili.com/video/BV1cy4y167mM  

```javasscript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var findSubsequences = function(nums) {
    let result = [];
    let path = [];
    function backtracing(startIndex) {
        if(path.length > 1) {
            result.push(path.slice())
            // 注意这里不要加return，要取树上的节点
        }
        let uset = new Set(); // 使用set对本层元素进行去重
        for(let i = startIndex; i < nums.length; i++) {
            if((path.length > 0 && nums[i] < path[path.length - 1]) || uset.has(nums[i])) {
                continue;
            }
            uset.add(nums[i]); // 记录这个元素在本层用过了，本层后面不能再用了
            path.push(nums[i]);
            backtracing(i + 1);
            path.pop();
        }
    }
    backtracing(0);
    return result;
};
```

## 49. Group Anagrams

https://leetcode.com/problems/group-anagra

文章链接：https://programmercarl.com/0046.%E5%85%A8%E6%8E%92%E5%88%97.html

视频讲解：https://www.bilibili.com/video/BV19v4y1S79W/

排列问题的不同：
- 每层都是从0开始搜索而不是startIndex
- 需要used数组记录path里都放了哪些元素了

<img width="1704" height="910" alt="image" src="https://github.com/user-attachments/assets/4d43adee-58b6-4f7c-bd76-e114416e5367" />

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function(nums) {
    let res = [];
    let path = [];
    function backtracking (n, used) {
        if (path.length == n.length) {
            res.push(path.slice());
            return;
        }
        for (let i = 0; i < n.length; i ++) {
            if (used[i] == true) continue; // path里已经收录的元素，直接跳过
            path.push(n[i]);
            used[i] = true;
            backtracking(n, used);
            path.pop();
            used[i] = false;
        }
    }
    backtracking(nums, [])
    return res;
};
```

## 47. Permutations II

https://leetcode.com/problems/permutations-ii/

需要去重，所以一定要对元素进行排序，这样我们才方便通过相邻的节点来判断是否重复使用了

<img width="1894" height="1098" alt="image" src="https://github.com/user-attachments/assets/c19b3313-3e60-4ab0-b7a7-2c10225877a1" />


```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permuteUnique = function (nums) {
    nums.sort(); // 排序
    let result = [];
    let path = [];

    function backtracing( used) {
        // 此时说明找到了一组
        if (path.length === nums.length) {
            result.push(path.slice());
            return;
        }
        for (let i = 0; i < nums.length; i++) {
            // used[i - 1] == true，说明同一树枝nums[i - 1]使用过
            // used[i - 1] == false，说明同一树层nums[i - 1]使用过
            // 如果同一树层nums[i - 1]使用过则直接跳过
            if (i > 0 && nums[i] === nums[i - 1] && !used[i - 1]) {
                continue;
            }
            if (!used[i]) {
                path.push(nums[i]);
                used[i] = true;
                backtracing(used);
                path.pop();
                used[i] = false;
            }
        }
    }
    backtracing([]);
    return result;
};
```
