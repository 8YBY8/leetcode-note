


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
