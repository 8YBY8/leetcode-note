# 第一章  数组part01 
https://programmercarl.com/%E6%95%B0%E7%BB%84%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html

## 704. Binary Search
https://leetcode.com/problems/binary-search/description/

文章讲解：https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html

视频讲解：https://www.bilibili.com/video/BV1fA4y1o715

Method 1: [l, r]
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums) - 1
        while l <= r:
            mid = l + (r - l) // 2
            if nums[mid] < target:
                l = mid + 1
            elif nums[mid] > target:
                r = mid - 1
            else: # nums[mid] == target
                return mid
        return -1
```

Method 2: [l, r)
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums) # [l, r)
        while l < r:
            mid = l  + (r - l) //2
            if nums[mid] < target:
                l = mid + 1
            elif nums[mid] > target:
                r = mid
            else:
                return mid
        
        return -1
```

## 27. Remove Element
https://leetcode.com/problems/remove-element/description/

文章讲解：https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html

视频讲解：https://www.bilibili.com/video/BV12A4y1Z7LP

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        # 快慢指针
        fast = 0  # 快指针
        slow = 0  # 慢指针
        size = len(nums)
        while fast < size:  # 不加等于是因为，a = size 时，nums[a] 会越界
            # slow 用来收集不等于 val 的值，如果 fast 对应值不等于 val，则把它与 slow 替换
            if nums[fast] != val:
                nums[slow] = nums[fast]
                slow += 1
            fast += 1
        return slow
```

## 977. Squares of a Sorted Array
https://leetcode.com/problems/squares-of-a-sorted-array/description/

文章讲解：https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html

视频讲解： https://www.bilibili.com/video/BV1QB4y1D7ep 


Method 1: 暴力
```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        for i in range(len(nums)):
            nums[i] = nums[i] ** 2
            # print(nums[i])
        
        return sorted(nums)
```
Method 2: two pointer
```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        res = [float('inf')] * len(nums)
        l, r = 0, len(nums) - 1
        i = len(nums) - 1
        while l <= r:
            if nums[l] ** 2 < nums[r] ** 2:
                res[i] = nums[r] ** 2
                r -= 1
            else: # nums[l] ** 2 > nums[r] ** 2
                res[i] = nums[l] ** 2
                l += 1
            i -= 1
        return res
```

# 第一章  数组part02
## 209. Minimum Size Subarray Sum
https://leetcode.com/problems/minimum-size-subarray-sum/description/ 

文章讲解：https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html 

视频讲解：https://www.bilibili.com/video/BV1tZ4y1q7XE
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        l, r = 0, 0
        minLen = float('inf')
        sumOfWid = 0
        while r <= len(nums) - 1:
            sumOfWid = sumOfWid + nums[r]
            while sumOfWid >= target:
                minLen = min(minLen, r - l + 1)
                sumOfWid -= nums[l]
                l += 1
            r += 1
        return minLen if minLen != float('inf') else 0
```

# 59. Spiral Matrix II
https://leetcode.com/problems/spiral-matrix-ii/description/

文章讲解：https://programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html

视频讲解：https://www.bilibili.com/video/BV1SL4y1N7mV/

<img width="314" height="238" alt="image" src="https://github.com/user-attachments/assets/be6d1f08-3136-474a-a75f-609ceaa92c0c" />

Method 1:
```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        if n <= 0:
            return []
        
        # 初始化 n x n 矩阵
        matrix = [[0]*n for _ in range(n)]

        # 初始化边界和起始值
        top, bottom, left, right = 0, n-1, 0, n-1
        num = 1

        while top <= bottom and left <= right:
            # 从左到右填充上边界
            for i in range(left, right + 1):
                matrix[top][i] = num
                num += 1
            top += 1

            # 从上到下填充右边界
            for i in range(top, bottom + 1):
                matrix[i][right] = num
                num += 1
            right -= 1

            # 从右到左填充下边界

            for i in range(right, left - 1, -1):
                matrix[bottom][i] = num
                num += 1
            bottom -= 1

            # 从下到上填充左边界

            for i in range(bottom, top - 1, -1):
                matrix[i][left] = num
                num += 1
            left += 1

        return matrix
```

Method 2:
```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        nums = [[0] * n for _ in range(n)]
        startx, starty = 0, 0               # 起始点
        loop, mid = n // 2, n // 2          # 迭代次数、n为奇数时，矩阵的中心点
        count = 1                           # 计数

        for offset in range(1, loop + 1) :      # 每循环一层偏移量加1，偏移量从1开始
            for i in range(starty, n - offset) :    # 从左至右，左闭右开
                nums[startx][i] = count
                count += 1
            for i in range(startx, n - offset) :    # 从上至下
                nums[i][n - offset] = count
                count += 1
            for i in range(n - offset, starty, -1) : # 从右至左
                nums[n - offset][i] = count
                count += 1
            for i in range(n - offset, startx, -1) : # 从下至上
                nums[i][starty] = count
                count += 1                
            startx += 1         # 更新起始点
            starty += 1

        if n % 2 != 0 :			# n为奇数时，填充中心点
            nums[mid][mid] = count 
        return nums
```


## 总结
数组：1. 下标都是从0开始的。2. 内存空间的地址是连续的。
二分法: left pointer and right pointer. `mid = left + (right - left) // 2 in Python`
双指针法（快慢指针法）：通过一个快指针和慢指针在一个for循环下完成两个for循环的工作。
滑动窗口: 滑动窗口的精妙之处在于根据当前子序列和大小的情况，不断调节子序列的起始位置。从而将O(n^2)的暴力解法降为O(n)

