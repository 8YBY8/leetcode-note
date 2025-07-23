# 栈与队列part01

https://programmercarl.com/%E6%A0%88%E4%B8%8E%E9%98%9F%E5%88%97%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html

队列queue是先进先出，栈stack是先进后出

<img width="524" height="286" alt="image" src="https://github.com/user-attachments/assets/da9c0aad-e89a-4b5d-9458-985dc211c5e8" />

<img width="556" height="310" alt="image" src="https://github.com/user-attachments/assets/26b291ae-64f8-4e42-8eb7-0344f01397e2" />

## 232. Implement Queue using Stacks

https://leetcode.com/problems/implement-queue-using-stacks/

文章链接：https://programmercarl.com/0232.%E7%94%A8%E6%A0%88%E5%AE%9E%E7%8E%B0%E9%98%9F%E5%88%97.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1nY4y1w7VC

![Implement Queue using Stacks](https://file1.kamacoder.com/i/algo/232.%E7%94%A8%E6%A0%88%E5%AE%9E%E7%8E%B0%E9%98%9F%E5%88%97%E7%89%88%E6%9C%AC2.gif)

```python
class MyQueue:
    # Initialize your data structure here
    def __init__(self):
        self.stackIn = []
        self.stackOut = []
    # Push element x to the back of queue
    def push(self, x: int) -> None:
        self.stackIn.append(x)
    # Removes the element from in front of queue and returns that element
    def pop(self) -> int:
        # 当stackIn和stackOut都为空的时候，return None
        if self.empty():
            return None
        
        if self.stackOut:
            return self.stackOut.pop()
        # 只有当stackOut为空的时候，再从stackIn里导入数据（导入stackIn全部数据）
        else:
            # 从stackIn导入数据直到stackIn为空
            for i in range(len(self.stackIn)):
                self.stackOut.append(self.stackIn.pop())
            return self.stackOut.pop()
    # Get the front element
    def peek(self) -> int:
        ans = self.pop() # 直接使用已有的pop函数
        self.stackOut.append(ans) # 因为pop函数弹出了元素res，所以再添加回去
        return ans
    # Returns whether the queue is empty
    def empty(self) -> bool:
        return not (self.stackIn or self.stackOut)


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```

## 225. Implement Stack using Queues

https://leetcode.com/problems/implement-stack-using-queues/

文章链接：https://programmercarl.com/0225.%E7%94%A8%E9%98%9F%E5%88%97%E5%AE%9E%E7%8E%B0%E6%A0%88.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1Fd4y1K7sm

```python
class MyStack:

    def __init__(self):
        self.que = deque()

    def push(self, x: int) -> None:
        self.que.append(x)

    def pop(self) -> int:
        if self.empty():
            return None
        # 将队列头部的元素（除了最后一个元素外） 重新添加到队列尾部
        for i in range(len(self.que)-1):
            self.que.append(self.que.popleft())
        # 此时弹出的元素顺序就是栈的顺序了
        return self.que.popleft()

    def top(self) -> int:
        # 写法一：
        if self.empty():
            return None
        return self.que[-1]

        # 写法二：
        # if self.empty():
        #     return None
        # # 将队列头部的元素（除了最后一个元素外） 重新添加到队列尾部
        # for i in range(len(self.que)-1):
        #     self.que.append(self.que.popleft())
        # temp = self.que.popleft() # 此时获得的元素就是栈顶的元素了
        # self.que.append(temp) #将获取完的元素也重新添加到队列尾部，保证数据结构没有变化
        # return temp

    def empty(self) -> bool:
        return not self.que
        


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```

## 20. Valid Parentheses

https://leetcode.com/problems/valid-parentheses/

文章链接：https://programmercarl.com/0020.%E6%9C%89%E6%95%88%E7%9A%84%E6%8B%AC%E5%8F%B7.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1AF411w78g

![Valid Parentheses](https://file1.kamacoder.com/i/algo/20.%E6%9C%89%E6%95%88%E6%8B%AC%E5%8F%B7.gif)

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        
        for item in s:
            if item == '(':
                stack.append(')')
            elif item == '[':
                stack.append(']')
            elif item == '{':
                stack.append('}')
            # 第三种情况：遍历字符串匹配的过程中，栈已经为空了，没有匹配的字符了，说明右括号没有找到对应的左括号 return false
            # 第二种情况：遍历字符串匹配的过程中，发现栈里没有我们要匹配的字符。所以return false
            elif not stack or stack[-1] != item:
                return False
            else:
                stack.pop()
        # 第一种情况：此时我们已经遍历完了字符串，但是栈不为空，说明有相应的左括号没有右括号来匹配，所以return false，否则就return true
        return True if not stack else False
```

## 1047. Remove All Adjacent Duplicates In String

https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/

文章链接：https://programmercarl.com/1047.%E5%88%A0%E9%99%A4%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%B8%AD%E7%9A%84%E6%89%80%E6%9C%89%E7%9B%B8%E9%82%BB%E9%87%8D%E5%A4%8D%E9%A1%B9.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV12a411P7mw?vd_source=dfe4be3e1289aa3263c6243a52315d05&spm_id_from=333.788.videopod.sections

```python
class Solution:
    def removeDuplicates(self, s: str) -> str:
        res = list()
        for item in s:
            if res and res[-1] == item:
                res.pop()
            else: # s 与 res.top()相等的情况
                res.append(item)
        return "".join(res)  # 字符串拼接
```

<img width="1275" height="569" alt="image" src="https://github.com/user-attachments/assets/99870f55-6622-4abb-9fdf-45e4e2d722c5" />

# 栈与队列part02

## 150. Evaluate Reverse Polish Notation

https://leetcode.com/problems/evaluate-reverse-polish-notation/

文章链接：https://programmercarl.com/0150.%E9%80%86%E6%B3%A2%E5%85%B0%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%B1%82%E5%80%BC.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1kd4y1o7on

![Evaluate Reverse Polish Notation](https://file1.kamacoder.com/i/algo/150.%E9%80%86%E6%B3%A2%E5%85%B0%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%B1%82%E5%80%BC.gif)

```javascript
/**
 * @param {string[]} tokens
 * @return {number}
 */
var evalRPN = function(tokens) {
    const stack = [];
    for (const token of tokens) {
        if (isNaN(Number(token))) { // 非数字
            // 出栈两个数字
            const n2 = stack.pop(); 
            const n1 = stack.pop();
            switch (token) {
                case "+":
                    stack.push(n1 + n2);
                    break;
                case "-":
                    stack.push(n1 - n2);
                    break;
                case "*":
                    stack.push(n1 * n2);
                    break;
                case "/":
                    stack.push(n1 / n2 | 0);
                    break;
            }
        } else { // 数字
            stack.push(Number(token));
        }
    }
    // 因没有遇到运算符而待在栈中的结果
    return stack[0]; 
};
```

## 239. Sliding Window Maximum

https://leetcode.com/problems/sliding-window-maximum/

文章链接：https://programmercarl.com/0239.%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3%E6%9C%80%E5%A4%A7%E5%80%BC.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1XS4y1p7qj

![Sliding Window Maximum](https://file1.kamacoder.com/i/algo/239.%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3%E6%9C%80%E5%A4%A7%E5%80%BC-2.gif)

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var maxSlidingWindow = function(nums, k) {
    class MonoQueue {
        queue; //单调队列（从大到小）
        constructor() {
            this.queue = [];
        }
        // 如果enqueue的数值大于入口元素的数值，那么就将队列后端的数值弹出，直到enqueue的数值小于等于队列入口元素的数值为止。
        // 这样就保持了队列里的数值是单调从大到小的了。
        enqueue(value) {
            let back = this.queue[this.queue.length - 1];
            while (back !== undefined && back < value) {
                this.queue.pop();
                back = this.queue[this.queue.length - 1];
            }
            this.queue.push(value);
        }
        // 每次弹出的时候，比较当前要弹出的数值是否等于队列出口元素的数值，如果相等则弹出。
        // 同时dequeue之前判断队列当前是否为空。
        dequeue(value) {
            let front = this.front();
            if (front === value) {
                this.queue.shift();
            }
        }
        // 查询当前队列里的最大值 直接返回队列前端
        front() {
            return this.queue[0];
        }
    }
    let helperQueue = new MonoQueue();
    let i = 0, j = 0;
    let resArr = [];
    while (j < k) { // 先将前k的元素放进队列
        helperQueue.enqueue(nums[j++]);
    }
    resArr.push(helperQueue.front()); // result 记录前k的元素的最大值
    while (j < nums.length) {
        helperQueue.dequeue(nums[i]); // 滑动窗口移除最前面元素
        helperQueue.enqueue(nums[j]); // 滑动窗口前加入最后面的元素
        resArr.push(helperQueue.front()); // 记录对应的最大值
        i++, j++;
    }
    return resArr;
};
```

## 347. Top K Frequent Elements

https://leetcode.com/problems/top-k-frequent-elements/

文章链接：https://programmercarl.com/0347.%E5%89%8DK%E4%B8%AA%E9%AB%98%E9%A2%91%E5%85%83%E7%B4%A0.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC

视频链接：https://www.bilibili.com/video/BV1Xg41167Lz

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var topKFrequent = function(nums, k) {
    const count = {};
    for (const num of nums) {
        count[num] = (count[num] || 0) + 1;
    }

    const arr = Object.entries(count).map(([num, freq]) => [freq, parseInt(num)]);
    arr.sort((a, b) => b[0] - a[0]);
    return arr.slice(0, k).map(pair => pair[1]);
};
```

# 总结

https://programmercarl.com/%E6%A0%88%E4%B8%8E%E9%98%9F%E5%88%97%E6%80%BB%E7%BB%93.html#%E6%A0%88%E4%B8%8E%E9%98%9F%E5%88%97%E7%9A%84%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80

一个队列在模拟栈弹出元素的时候只要将队列头部的元素（除了最后一个元素外） 重新添加到队列尾部，此时在去弹出元素就是栈的顺序了

