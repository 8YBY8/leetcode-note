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
