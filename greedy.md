[贪心算法 part01](https://github.com/8YBY8/leetcode-note/blob/main/greedy.md#%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95-part01)

[贪心算法 part02](https://github.com/8YBY8/leetcode-note/blob/main/greedy.md#%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95-part02)

[贪心算法 part03](https://github.com/8YBY8/leetcode-note/blob/main/greedy.md#%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95-part03)

[贪心算法 part04](https://github.com/8YBY8/leetcode-note/blob/main/greedy.md#%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95-part04)

# 贪心算法 part01
## 理论基础
https://programmercarl.com/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html

<img width="992" height="986" alt="image" src="https://github.com/user-attachments/assets/d23775cc-03cc-4593-81f3-b6e2ad2af3c0" />

贪心没有套路，说白了就是常识性推导加上举反例。

贪心的思考方式（局部最优，全局最优）

局部最优可以推出全局最优。

## 455. Assign Cookies

https://leetcode.com/problems/assign-cookies/

https://programmercarl.com/0455.%E5%88%86%E5%8F%91%E9%A5%BC%E5%B9%B2.html

想清楚局部最优，想清楚全局最优，感觉局部最优是可以推出全局最优，并想不出反例，那么就试一试贪心

```javasript
/**
 * @param {number[]} g
 * @param {number[]} s
 * @return {number}
 */
var findContentChildren = function (g, s) {
    // 小饼干先喂饱小胃口
    g = g.sort((a, b) => a - b);
    s = s.sort((a, b) => a - b);
    console.log(g, s)
    let index = 0;
    let result = 0;
    for (let i = 0; i < s.length; i++) { // 饼干
        if (index < g.length && g[index] <= s[i]) { // 胃口
            index++;
            result++;
        }
    }
    return result;
};
```

## 376. Wiggle Subsequence

https://leetcode.com/problems/wiggle-subsequence/

https://programmercarl.com/0376.%E6%91%86%E5%8A%A8%E5%BA%8F%E5%88%97.html

我们只需要在 这个坡度 摆动变化的时候，更新 prediff 就行，这样 prediff 在 单调区间有平坡的时候 就不会发生变化，造成我们的误判。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var wiggleMaxLength = function (nums) {
    if (nums.length <= 1) return nums.length
    let result = 1;  // 记录峰值个数，序列默认序列最右边有一个峰值
    let preDiff = 0; // 前一对差值
    let curDiff = 0; // 当前一对差值
    for (let i = 0; i < nums.length - 1; i++) {
        curDiff = nums[i + 1] - nums[i];
        // 出现峰值
        if ((curDiff > 0 && preDiff <= 0) || (curDiff < 0 && preDiff >= 0)) {
            result++;
            preDiff = curDiff; // 注意这里，只在摆动变化的时候更新prediff。这样 prediff 在 单调区间有平坡的时候 就不会发生变化，造成我们的误判
        }
    }
    return result;
};
```

## 53. Maximum Subarray

https://leetcode.com/problems/maximum-subarray/

https://programmercarl.com/0053.%E6%9C%80%E5%A4%A7%E5%AD%90%E5%BA%8F%E5%92%8C.html

![Maximum Subarray](https://file1.kamacoder.com/i/algo/53.%E6%9C%80%E5%A4%A7%E5%AD%90%E5%BA%8F%E5%92%8C.gif)

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function (nums) {
    let result = -Infinity
    let count = 0
    for (let i = 0; i < nums.length; i++) {
        count += nums[i]
        if (count > result) { // 取区间累计的最大值（相当于不断确定最大子序终止位置）
            result = count
        }
        if (count < 0) { // 相当于重置最大子序起始位置，因为遇到负数一定是拉低总和
            count = 0
        }
    }
    return result
};
```

# 贪心算法 part02

## 122. Best Time to Buy and Sell Stock II

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

本题中理解利润拆分是关键点！ 不要整块的去看，而是把整体利润拆为每天的利润

<img width="978" height="572" alt="image" src="https://github.com/user-attachments/assets/cfd072b3-edb1-4880-8aa8-c5af5f4597be" />

收集每天的正利润

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
    let result = 0;
    for (let i = 1; i < prices.length; i++) {
        result += Math.max(prices[i] - prices[i - 1], 0); // 收集每天的正利润
    }
    return result;
};
```

## 55. Jump Game

https://leetcode.com/problems/jump-game/

不用拘泥于每次究竟跳几步，而是看覆盖范围，覆盖范围内一定是可以跳过来的，不用管是怎么跳的

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var canJump = function (nums) {
    if (nums.length === 1) return true; // 只有一个元素，就是能达到
    let cover = 0;
    for (let i = 0; i <= cover; i++) { // 注意这里是小于等于cover
        cover = Math.max(cover, i + nums[i]);
        if (cover >= nums.length - 1) {
            return true; // 说明可以覆盖到终点了
        }
    }
    return false;
};
```

## 45. Jump Game II

https://leetcode.com/problems/jump-game-ii/

移动下标只要遇到当前覆盖最远距离的下标，直接步数加一，不考虑是不是终点的情况

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var jump = function (nums) {
    let curIndex = 0; // 当前覆盖最远距离下标
    let nextIndex = 0; // 下一步覆盖最远距离下标
    let steps = 0; // 记录走的最大步数
    for (let i = 0; i < nums.length - 1; i++) { // 注意这里是小于nums.size() - 1，这是关键所在
        nextIndex = Math.max(nums[i] + i, nextIndex); // 更新下一步覆盖最远距离下标
        if (i === curIndex) { // 遇到当前覆盖最远距离下标
            curIndex = nextIndex; // 更新当前覆盖最远距离下标（相当于加油了）
            steps++; // 需要走下一步
        }
    }

    return steps;
};
```

## 1005. Maximize Sum Of Array After K Negations

https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/

本题的解题步骤为：
- 第一步：将数组按照绝对值大小从大到小排序，注意要按照绝对值的大小
- 第二步：从前向后遍历，遇到负数将其变为正数，同时K--
- 第三步：如果K还大于0，那么反复转变数值最小的元素，将K用完
- 第四步：求和

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var largestSumAfterKNegations = function (nums, k) {
    // 将数组按照绝对值大小从大到小排序
    nums.sort((a, b) => Math.abs(b) - Math.abs(a));

    // 从前向后遍历，遇到负数将其变为正数，同时K--
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] < 0 && k > 0) {
            nums[i] = - nums[i];
            k--;
        }
    }

    // 如果K还大于0，那么反复转变数值最小的元素，将K用完
    while (k > 0) {
        nums[nums.length - 1] = - nums[nums.length - 1];
        k--;
    }

    // 求和
    // 使用箭头函数的隐式返回值时，需使用简写省略花括号，否则要在 a + b 前加上 return
    return nums.reduce((a, b) => a + b);
};
```

# 贪心算法 part03

## 134. Gas Station

https://leetcode.com/problems/gas-station/

https://programmercarl.com/0134.%E5%8A%A0%E6%B2%B9%E7%AB%99.html

首先如果总油量减去总消耗大于等于零那么一定可以跑完一圈

局部最优：当前累加`gas[i] - cost[i]`的和`curSum`一旦小于0，起始位置至少要是i+1，因为从i之前开始一定不行。全局最优：找到可以跑一圈的起始位置

```javascript
/**
 * @param {number[]} gas
 * @param {number[]} cost
 * @return {number}
 */
var canCompleteCircuit = function (gas, cost) {
    const gasLen = gas.length
    let start = 0
    let curSum = 0
    let totalSum = 0

    for (let i = 0; i < gasLen; i++) {
        curSum += gas[i] - cost[i]
        totalSum += gas[i] - cost[i]
        // 当前gas[i] - cost[i]和curSum一旦小于0
        if (curSum < 0) { 
            curSum = 0    // curSum从0开始
            start = i + 1 // 起始位置更新为i+1
        }
    }

    if (totalSum < 0) return -1 // 说明怎么走都不可能跑一圈了

    return start
};
```

<img width="1236" height="982" alt="image" src="https://github.com/user-attachments/assets/28c07f93-0fed-479d-81fa-cec7e17aa9f7" />

分两个阶段:
1. 起点下标1 从左往右，只要 当前 比 左边 大，当前的糖果=左边的糖果 + 1
2. 起点下标 ratings.length - 2 从右往左， 只要 当前 比 右边 大，此时 当前的糖果应该 取本身的糖果数（符合比它左边大） 和 右边糖果数 + 1 二者的最大值，这样才符合 它比它左边的大，也比它右边大

```javascript
/**
 * @param {number[]} ratings
 * @return {number}
 */
var candy = function(ratings) {
    let candys = new Array(ratings.length).fill(1)
    // 从前向后
    for(let i = 1; i < ratings.length; i++) {
        if(ratings[i] > ratings[i - 1]) {
            candys[i] = candys[i - 1] + 1
        }
    }
    // 从后向前
    for(let i = ratings.length - 2; i >= 0; i--) {
        if(ratings[i] > ratings[i + 1]) {
            candys[i] = Math.max(candys[i], candys[i + 1] + 1)
        }
    }
    // 统计结果
    let count = candys.reduce((a, b) => {
        return a + b
    })

    return count
};
```

## 860. Lemonade Change

https://leetcode.com/problems/lemonade-change/

有如下三种情况：
- 情况一：账单是5，直接收下。
- 情况二：账单是10，消耗一个5，增加一个10
- 情况三：账单是20，优先消耗一个10和一个5，如果不够，再消耗三个5

```javascript
/**
 * @param {number[]} bills
 * @return {boolean}
 */
var lemonadeChange = function (bills) {
    let fiveCount = 0
    let tenCount = 0

    for (let i = 0; i < bills.length; i++) {
        let bill = bills[i]
        // 账单是5，直接收下
        if (bill === 5) {
            fiveCount += 1
            // 账单是10，消耗一个5，增加一个10
        } else if (bill === 10) {
            if (fiveCount > 0) {
                fiveCount -= 1
                tenCount += 1
            } else {
                return false
            }
            // 账单是20，优先消耗一个10和一个5，如果不够，再消耗三个5
        } else {
            if (tenCount > 0 && fiveCount > 0) {
                tenCount -= 1
                fiveCount -= 1
            } else if (fiveCount >= 3) {
                fiveCount -= 3
            } else {
                return false
            }
        }
    }
    return true
};
```

## 406. Queue Reconstruction by Height

https://leetcode.com/problems/queue-reconstruction-by-height/

技巧是确定一边然后贪心另一边，两边一起考虑，就会顾此失彼

```javascript
/**
 * @param {number[][]} people
 * @return {number[][]}
 */
var reconstructQueue = function(people) {
    let queue = []
    people.sort((a, b ) => {
        if(b[0] !== a[0]) {
            return b[0] - a[0] //b - a 是降序排列，在a[0] != b[0]，的狀況會根據h值降序排列
        } else {
            return a[1] - b[1] // a - b 是升序排列，故在a[0] == b[0]的狀況下，會根據k值升序排列
        }
        
    })

    for(let i = 0; i < people.length; i++) {
        queue.splice(people[i][1], 0, people[i]) 
        // this takes the i-th person and inserts them into queue at the position specified by their second value (people[i][1]).
        // The second argument to splice means delete 0 elements
    }
    return queue
};
```

# 贪心算法 part04

## 452. Minimum Number of Arrows to Burst Balloons

https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/

https://programmercarl.com/0452.%E7%94%A8%E6%9C%80%E5%B0%91%E6%95%B0%E9%87%8F%E7%9A%84%E7%AE%AD%E5%BC%95%E7%88%86%E6%B0%94%E7%90%83.html

<img width="1488" height="938" alt="image" src="https://github.com/user-attachments/assets/54ee0e9d-c86b-4f6d-97f5-9c8ce45dddbc" />

<img width="812" height="512" alt="image" src="https://github.com/user-attachments/assets/96a572c8-890a-40e9-9f9a-8f4e5f0b6d98" />


```javascript
/**
 * @param {number[][]} points
 * @return {number}
 */
var findMinArrowShots = function (points) {
    // 根据气球直径的开始坐标从小到大排序
    points.sort((a, b) => {
        return a[0] - b[0]
    })
    let result = 1 // points 不为空至少需要一支箭
    for (let i = 1; i < points.length; i++) {
        // 气球i和气球i-1不挨着，注意这里不是>=
        if (points[i][0] > points[i - 1][1]) { 
            result++ // 需要一支箭
        // 气球i和气球i-1挨着
        } else { 
            points[i][1] = Math.min(points[i - 1][1], points[i][1]) // 更新重叠气球最小右边界
        }
    }

    return result
};
```

## 435. Non-overlapping Intervals

https://leetcode.com/problems/non-overlapping-intervals/

https://programmercarl.com/0435.%E6%97%A0%E9%87%8D%E5%8F%A0%E5%8C%BA%E9%97%B4.html

按照右边界排序，从左向右记录非交叉区间的个数。最后用区间总数减去非交叉区间的个数就是需要移除的区间个数了

<img width="1126" height="518" alt="image" src="https://github.com/user-attachments/assets/66801436-df0b-433d-8bf0-3939f0de4da1" />

```javascript
/**
 * @param {number[][]} intervals
 * @return {number}
 */
var eraseOverlapIntervals = function (intervals) {
    // 右边界排序
    intervals.sort((a, b) => {
        return a[1] - b[1]
    })

    let count = 1 // 记录非交叉区间的个数
    let end = intervals[0][1] // 记录区间分割点

    for (let i = 1; i < intervals.length; i++) {
        let interval = intervals[i]
        if (interval[0] >= end) { //重叠情况
            end = interval[1]
            count += 1
        }
    }
    // count 记录的是最大非重复区间的个数
    return intervals.length - count
};
```

## 763. Partition Labels

https://leetcode.com/problems/partition-labels/

https://programmercarl.com/0763.%E5%88%92%E5%88%86%E5%AD%97%E6%AF%8D%E5%8C%BA%E9%97%B4.html

可以分为如下两步：
1. 统计每一个字符最后出现的位置
2. 从头遍历字符，并更新字符的最远出现下标，如果找到字符最远出现位置下标和当前下标相等了，则找到了分割点

<img width="1430" height="564" alt="image" src="https://github.com/user-attachments/assets/099914a8-b005-40ab-87e0-e721d56a0892" />

```javascript
/**
 * @param {string} s
 * @return {number[]}
 */
var partitionLabels = function (s) {
    let hash = {} // i为字符，hash[s[i]]为字符出现的最后位置
    // 统计每一个字符最后出现的位置
    for (let i = 0; i < s.length; i++) {
        hash[s[i]] = i
    }
    let result = []
    let left = 0
    let right = 0
    // 从头遍历字符
    for (let i = 0; i < s.length; i++) {
        right = Math.max(right, hash[s[i]]) // 找到字符出现的最远边界
        // 如果找到字符最远出现位置下标和当前下标相等了，则找到了分割点
        if (right === i) { 
            result.push(right - left + 1)
            left = i + 1
        }
    }
    return result
};
```
