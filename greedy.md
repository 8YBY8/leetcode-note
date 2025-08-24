[贪心算法 part01](https://github.com/8YBY8/leetcode-note/blob/main/greedy.md#%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95-part01)

[贪心算法 part02](https://github.com/8YBY8/leetcode-note/blob/main/greedy.md#%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95-part02)



# 贪心算法 part01
## 理论基础
https://programmercarl.com/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html

<img width="992" height="986" alt="image" src="https://github.com/user-attachments/assets/d23775cc-03cc-4593-81f3-b6e2ad2af3c0" />

贪心没有套路，说白了就是常识性推导加上举反例。

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
