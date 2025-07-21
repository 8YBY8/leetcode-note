# 字符串part01

## 344. Reverse String

https://leetcode.com/problems/reverse-string/

文章链接：https://programmercarl.com/0344.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1fV4y17748

Method 1: 双指针

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left, right = 0, len(s) - 1
        
        # 该方法已经不需要判断奇偶数，经测试后时间空间复杂度比用 for i in range(len(s)//2)更低
        # 因为while每次循环需要进行条件判断，而range函数不需要，直接生成数字，因此时间复杂度更低。推荐使用range
        while left < right:
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1
```

Method 2: 使用range

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        n = len(s)
        for i in range(n // 2):
            s[i], s[n - i - 1] = s[n - i - 1], s[i]
```

Method 3: 使用reversed

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        s[:] = reversed(s)
```

## 541. Reverse String II

https://leetcode.com/problems/reverse-string-ii/

文章链接：https://programmercarl.com/0541.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2II.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1dT411j7NN

Method 1: 通用于其他语言的解法

```python
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        # 1. 使用range(start, end, step)来确定需要调换的初始位置
        # 2. 对于字符串s = 'abc'，如果使用s[0:999] ===> 'abc'。字符串末尾如果超过最大长度，则会返回至字符串最后一个值，这个特性可以避免一些边界条件的处理。
        # 3. 用切片整体替换，而不是一个个替换.
        def reverse_substring(text):
            left, right = 0, len(text) - 1
            while left < right:
                text[left], text[right] = text[right], text[left]
                left += 1
                right -= 1
            return text
        
        res = list(s)

        for cur in range(0, len(s), 2 * k):
            res[cur: cur + k] = reverse_substring(res[cur: cur + k])

        return ''.join(res)
```

Method 2: 通用于其他语言的解法 + reversed()

```
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        t = list(s)
        for i in range(0, len(t), 2 * k):
            t[i: i + k] = reversed(t[i: i + k])
        return "".join(t)

作者：力扣官方题解
链接：https://leetcode.cn/problems/reverse-string-ii/solutions/946553/fan-zhuan-zi-fu-chuan-ii-by-leetcode-sol-ua7s/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

Method 3：Python特性

```python
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        # Two pointers. Another is inside the loop.
        p = 0
        while p < len(s):
            p2 = p + k
            # Written in this could be more pythonic.
            s = s[:p] + s[p: p2][::-1] + s[p2:]
            p = p + 2 * k
        return s
```

## 卡码网：54.替换数字 

https://kamacoder.com/problempage.php?pid=1064

文章链接：https://programmercarl.com/kamacoder/0054.%E6%9B%BF%E6%8D%A2%E6%95%B0%E5%AD%97.html

```python
class Solution(object):
    def subsitute_numbers(self, s):
        """
        :type s: str
        :rtype: str
        """
        
        count = sum(1 for char in s if char.isdigit()) # 统计数字的个数
        expand_len = len(s) + (count * 5)  # 计算扩充后字符串的大小， x->number， 每有一个数字就要增加五个长度
        res = [''] * expand_len
        
        new_index = expand_len - 1 # 指向扩充后字符串末尾
        old_index = len(s) - 1 # 指向原字符串末尾
        
        while old_index >= 0: # 从后往前， 遇到数字替换成“number”
            if s[old_index].isdigit():
                res[new_index-5:new_index+1] = "number"
                new_index -= 6
            else:
                res[new_index] = s[old_index]
                new_index -= 1
            old_index -= 1
        
        return "".join(res)
        
if __name__ == "__main__":
    solution = Solution()

    while True:
        try:
            s = input()
            result = solution.subsitute_numbers(s)
            print(result)
        except EOFError:
            break
```

# 字符串part02

## 151. Reverse Words in a String

https://leetcode.com/problems/reverse-words-in-a-string/

文章链接：https://programmercarl.com/0151.%E7%BF%BB%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2%E9%87%8C%E7%9A%84%E5%8D%95%E8%AF%8D.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1uT41177fX

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        # return " ".join(reversed(s.split()))
        newS = s.split()
        reveS = reversed(newS)
        return " ".join(reveS)
```

## 卡码网：55.右旋转字符串 

https://kamacoder.com/problempage.php?pid=1065

文章链接：https://programmercarl.com/kamacoder/0055.%E5%8F%B3%E6%97%8B%E5%AD%97%E7%AC%A6%E4%B8%B2.html#%E6%80%9D%E8%B7%AF

```python
#获取输入的数字k和字符串
k = int(input())
s = input()

#通过切片反转第一段和第二段字符串
#注意：python中字符串是不可变的，所以也需要额外空间
s = s[len(s)-k:] + s[:len(s)-k]
print(s)
```

## 28. Find the Index of the First Occurrence in a String

https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/

文章链接：https://programmercarl.com/0028.%E5%AE%9E%E7%8E%B0strStr.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1PD4y1o7nd/ https://www.bilibili.com/video/BV1M5411j7Xx

Method 1: 使用 find (最简单)

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        return haystack.find(needle)
```

Method 2：使用KMP 前缀表（减一）

```python
class Solution:
    def getNext(self, next, s):
        j = -1
        next[0] = j
        for i in range(1, len(s)):
            while j >= 0 and s[i] != s[j+1]:
                j = next[j]
            if s[i] == s[j+1]:
                j += 1
            next[i] = j
    
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle:
            return 0
        next = [0] * len(needle)
        self.getNext(next, needle)
        j = -1
        for i in range(len(haystack)):
            while j >= 0 and haystack[i] != needle[j+1]:
                j = next[j]
            if haystack[i] == needle[j+1]:
                j += 1
            if j == len(needle) - 1:
                return i - len(needle) + 1
        return -1
```

## 459. Repeated Substring Pattern

https://leetcode.com/problems/repeated-substring-pattern/

文章链接：https://programmercarl.com/0459.%E9%87%8D%E5%A4%8D%E7%9A%84%E5%AD%90%E5%AD%97%E7%AC%A6%E4%B8%B2.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1cg41127fw/?vd_source=dfe4be3e1289aa3263c6243a52315d05

Method 1: 使用 find

解题思路：
- 通过复制两个s创建ss并去头去尾
- 如果ss里有s，那return True

```python
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        n = len(s)
        if n <= 1:
            return False
        # 通过复制两个s创建ss并去头去尾
        # 如果ss里有s，那return True
        ss = s[1:] + s[:-1] 
        return ss.find(s) != -1
```

Method 2: 使用KMP 前缀表减一

```python
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:  
        if len(s) == 0:
            return False
        nxt = [0] * len(s)
        self.getNext(nxt, s)
        if nxt[-1] != -1 and len(s) % (len(s) - (nxt[-1] + 1)) == 0:
            return True
        return False
    
    def getNext(self, nxt, s):
        nxt[0] = -1
        j = -1
        for i in range(1, len(s)):
            while j >= 0 and s[i] != s[j+1]:
                j = nxt[j]
            if s[i] == s[j+1]:
                j += 1
            nxt[i] = j
        return nxt
```

# 总结

## 字符串

字符串：若干字符组成的有限序列，也可以理解为是一个字符数组

要不要使用库函数：如果题目关键的部分直接用库函数就可以解决，建议不要使用库函数。如果库函数仅仅是 解题过程中的一小部分，并且你已经很清楚这个库函数的内部实现原理的话，可以考虑使用库函数。

当需要固定规律一段一段去处理字符串的时候，要想想在在for循环的表达式上做做文章。比如 i += (2 * k)，i 每次移动 2 * k 

KMP:
- 前缀：指不包含最后一个字符的所有以第一个字符开头的连续子串。
- 后缀：指不包含第一个字符的所有以最后一个字符结尾的连续子串。

## 双指针

### 数组篇

使用双指针法效率的优势：通过两个指针在一个for循环下完成两个for循环的工作。

### 字符串篇

使用双指针法，定义两个指针（也可以说是索引下标），一个从字符串前面，一个从字符串后面，两个指针同时向中间移动，并交换元素。

其实很多数组（字符串）填充类的问题，都可以先预先给数组扩容带填充后的大小，然后在从后向前进行操作。

### 链表篇

只需要改变链表的next指针的指向，直接将链表反转 ，而不用重新定义一个新的链表

使用快慢指针（双指针法），分别定义 fast 和 slow指针，从头结点出发，fast指针每次移动两个节点，slow指针每次移动一个节点，如果 fast 和 slow指针在途中相遇 ，说明这个链表有环。

### N数之和篇

三数之和：通过前后两个指针不断向中间逼近，在一个for循环下完成两个for循环的工作。

四数之和：在三数之和的基础上再套一层for循环，依然是使用双指针法。同样的道理，五数之和，n数之和都是在这个基础上累加。

除了链表一些题目一定要使用双指针，其他题目都是使用双指针来提高效率，一般是将O(n^2)的时间复杂度，降为 $O(n)$ 。
