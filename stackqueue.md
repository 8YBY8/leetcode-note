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


