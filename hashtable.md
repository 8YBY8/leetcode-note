# 哈希表part01

https://programmercarl.com/%E5%93%88%E5%B8%8C%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html#%E5%93%88%E5%B8%8C%E8%A1%A8

当我们遇到了要快速判断一个元素是否出现集合里的时候，就要考虑哈希法。

但是哈希法也是牺牲了空间换取了时间，因为我们要使用额外的数组，set或者是map来存放数据，才能实现快速的查找。

如果在做面试题目的时候遇到需要判断一个元素是否出现过的场景也应该第一时间想到哈希法

## 242. Valid Anagram

https://leetcode.com/problems/valid-anagram/

文章链接：https://programmercarl.com/0242.%E6%9C%89%E6%95%88%E7%9A%84%E5%AD%97%E6%AF%8D%E5%BC%82%E4%BD%8D%E8%AF%8D.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1YG411p7BA/

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t): # 如果s和t不一样长他们就不是Anagram
            return False

        countS, countT = {}, {} # 储存出现频率

        # 遍历一边把字母的出现频率加进去
        for i in range(len(s)):
            countS[s[i]] = 1 + countS.get(s[i], 0)
            countT[t[i]] = 1 + countT.get(t[i], 0)
        return countS == countT # 比较每个字母的数量是不是一样
```

## 349. Intersection of Two Arrays

https://leetcode.com/problems/intersection-of-two-arrays/

文章链接：https://programmercarl.com/0349.%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E4%BA%A4%E9%9B%86.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1ba411S7wu/

```python
# 使用哈希表存储一个数组中的所有元素
        table = {}
        for num in nums1:
            table[num] = table.get(num, 0) + 1
        
        # 使用集合存储结果
        res = set()
        for num in nums2:
            if num in table:
                res.add(num)
                del table[num]
        
        return list(res)
```

## 202. Happy Number

https://leetcode.com/problems/happy-number/

文章链接：https://programmercarl.com/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.html#%E6%80%9D%E8%B7%AF

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        record = set()

        while True:
            n = self.get_sum(n)
            if n == 1:
                return True
            
            # 如果中间结果重复出现，说明陷入死循环了，该数不是快乐数
            if n in record:
                return False
            else:
                record.add(n)

    def get_sum(self,n: int) -> int: 
        new_num = 0
        while n:
            n, r = divmod(n, 10) # divmod(a, b) return (a // b, a % b)
            new_num += r ** 2
        return new_num
```

## 1. Two Sum

https://leetcode.com/problems/two-sum/

文章链接：https://programmercarl.com/0001.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC

视频链接：https://www.bilibili.com/video/BV1ba411S7wu/

什么时候使用哈希法map{}：当我们需要查询一个元素是否出现过，或者一个元素是否在集合里的时候，就要第一时间想到哈希法

因为本题，我们不仅要知道元素有没有遍历过，还要知道这个元素对应的下标，需要使用 key value结构来存放，key来存元素，value来存下标，那么使用map正合适。

再来看一下使用数组和set来做哈希法的局限。
- 数组的大小是受限制的，而且如果元素很少，而哈希值太大会造成内存空间的浪费。
- set是一个集合，里面放的元素只能是一个key，而两数之和这道题目，不仅要判断y是否存在而且还要记录y的下标位置，因为要返回x 和 y的下标。所以set 也不能用

map中的存储结构为 {key：数据元素，value：数组元素对应的下标}
在遍历数组的时候，只需要向map去查询是否有和目前遍历元素匹配的数值，如果有，就找到的匹配对，如果没有，就把目前遍历的元素放进map中，因为map存放的就是我们访问过的元素。

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        #创建一个集合来存储我们目前看到的数字
        prevMap = {}  # val -> index
        for i, n in enumerate(nums):
            diff = target - n
            if diff in prevMap:
                return [prevMap[diff], i]
            prevMap[n] = i
```

# 哈希表part02 

## 454. 4Sum II

https://leetcode.com/problems/4sum-ii/

文章链接：https://programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html

视频链接：https://www.bilibili.com/video/BV1Md4y1Q7Yh

- 第一步：创建Map数组集合，key用来存放前两个数组的元素和，value用来存放和出现过的次数
- 第二步：遍历前两个数组，将和：出现过的次数存放发哦Map集合中
- 第三步：遍历后两个数组，将满足条件的情况记录到result中。

```python
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        temp = {} # store the [nums1[i] + nums2[j], n]
        count = 0

        # 遍历nums1和nums2，把nums1[i] + nums2[j]的个数存到temp里
        for n1 in nums1:
            for n2 in nums2:
                temp[n1 + n2] = temp.get(n1 + n2, 0) + 1

        # 如果 -(n1+n2) 存在于nums3和nums4, 存入结果    
        for n3 in nums3:
            for n4 in nums4:
                if (- n3 - n4) in temp:
                    count += temp.get(- n3 - n4, 0)
                
        return count
```

## 383. Ransom Note

https://leetcode.com/problems/ransom-note/

文章链接：https://programmercarl.com/0383.%E8%B5%8E%E9%87%91%E4%BF%A1.html#%E6%80%9D%E8%B7%AF

- 第一步：创建Map集合
- 第二步：遍历magazine，记录字符和每个字符出现次数
- 第三步：遍历ransomNote，将Map集合中对应字符出现的次数减去，如果出现了次数<0的字符，就返回false

```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        if len(ransomNote) > len(magazine):
            return False

        counts = {}
        # 通过record数据记录 magazine里各个字符出现次数
        for c in magazine:
            counts[c] = counts.get(c, 0) + 1
        # 遍历ransomNote，在record里对应的字符个数做一一操作
        for c in ransomNote:
            if c not in counts or counts[c] == 0:
                return False
            counts[c] -= 1
        return True
```

## 15. 3Sum

https://leetcode.com/problems/3sum/

文章链接：https://programmercarl.com/0015.%E4%B8%89%E6%95%B0%E4%B9%8B%E5%92%8C.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1GW4y127qo

![3Sum gif](https://file1.kamacoder.com/i/algo/15.%E4%B8%89%E6%95%B0%E4%B9%8B%E5%92%8C.gif)

- 第一步：创建接收集合，对数组进行排序
- 第二步：遍历数组，有了指针i
- 第三步：对指针 i 进行去重操作
- 第四步：创建left 和 right 指针
- 第五步：移动指针，找到符合条件的元素
- 第六步：如果找到，收割结果，对left和right进行去重操作
- 第七步：继续移动指针寻找符合条件的元组

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        result = []
        nums.sort()
        
        for i in range(len(nums)):
            # 如果第一个元素已经大于0，不需要进一步检查
            if nums[i] > 0:
                return result
            
            # 跳过相同的元素以避免重复
            if i > 0 and nums[i] == nums[i - 1]:
                continue
                
            left = i + 1
            right = len(nums) - 1
            
            while right > left:
                sum_ = nums[i] + nums[left] + nums[right]
                
                if sum_ < 0:
                    left += 1
                elif sum_ > 0:
                    right -= 1
                else:
                    result.append([nums[i], nums[left], nums[right]])
                    
                    # 跳过相同的元素以避免重复
                    while right > left and nums[right] == nums[right - 1]:
                        right -= 1
                    while right > left and nums[left] == nums[left + 1]:
                        left += 1
                        
                    right -= 1
                    left += 1
                    
        return result
```

## 18. 4Sum

https://leetcode.com/problems/4sum/description/

文章链接：https://programmercarl.com/0018.%E5%9B%9B%E6%95%B0%E4%B9%8B%E5%92%8C.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1DS4y147US

<img width="792" height="642" alt="image" src="https://github.com/user-attachments/assets/f9f6a475-0724-42a7-b258-6367961dddcd" />

- 第一步：创建接收集合，对数组进行排序
- 第二步：遍历第一个元素，对k进行剪枝和去重
- 第三步：遍历第二个元素，对i进行剪枝和去重
- 第四步：定义left和right指针
- 第五步：移动指针，找到符合条件的元素
- 第六步：如果找到，收割结果，对left和right进行去重操作
- 第七步：继续移动指针寻找符合条件的元组

```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        n = len(nums)
        result = []
        for i in range(n):
            # 剪枝（可省）
            if nums[i] > target and nums[i] > 0 and target > 0:
                break # 这里使用break，统一通过最后的return返回
            # 对nums[i]去重
            if i > 0 and nums[i] == nums[i-1]:
                continue
            for j in range(i+1, n):
                # 2级剪枝处理（可省）
                if nums[i] + nums[j] > target and target > 0: 
                    break
                # 对nums[j]去重去重
                if j > i+1 and nums[j] == nums[j-1]: 
                    continue
                left, right = j+1, n-1
                while left < right:
                    s = nums[i] + nums[j] + nums[left] + nums[right]
                    if s == target:
                        # 加答案
                        result.append([nums[i], nums[j], nums[left], nums[right]])
                        
                        # 对nums[left]和nums[right]去重
                        while left < right and nums[left] == nums[left+1]:
                            left += 1
                        while left < right and nums[right] == nums[right-1]:
                            right -= 1
                        
                        # 找到答案时，双指针同时收缩
                        left += 1
                        right -= 1
                    # nums[i] + nums[j] + nums[left] + nums[right] < target 会溢出
                    elif s < target:
                        left += 1
                    # nums[i] + nums[j] + nums[left] + nums[right] > target 会溢出
                    else:
                        right -= 1
        return result
```

# 总结

什么时候使用哈希法map{}：当我们需要查询一个元素是否出现过，或者一个元素是否在集合里的时候，就要第一时间想到哈希法
