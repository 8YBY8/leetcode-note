# 链表part01
https://programmercarl.com/%E9%93%BE%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html#%E9%93%BE%E8%A1%A8%E7%9A%84%E7%B1%BB%E5%9E%8B

单链表:
- 一种通过指针串联在一起的线性结构，每一个节点由两部分组成，一个是数据域一个是指针域（存放指向下一个节点的指针），最后一个节点的指针域指向null（空指针的意思）。
- 链表的入口节点称为链表的头结点也就是head。
- 只向后查询

<img width="1118" height="360" alt="image" src="https://github.com/user-attachments/assets/6d28af97-e7c9-45cb-8b19-a4f2e4981af4" />

定义链表节点

```python
class ListNode:
    def __init__(self, val, next=None):
        self.val = val
        self.next = next
```

双链表: 
- 每一个节点有两个指针域，一个指向下一个节点，一个指向上一个节点。
- 既可以向前查询也可以向后查询。

<img width="1192" height="276" alt="image" src="https://github.com/user-attachments/assets/85d1edb7-0dd8-4c65-a182-a473c2c50377" />

循环链表: 链表首尾相连

<img width="514" height="440" alt="image" src="https://github.com/user-attachments/assets/53487d02-f958-4e24-ad78-a96372301747" />

### 删除节点
删除D节点，如图所示：
<img width="1132" height="308" alt="image" src="https://github.com/user-attachments/assets/b97bce87-ea6e-44e2-b0a9-66812e7f9b72" />
添加节点
<img width="1122" height="420" alt="image" src="https://github.com/user-attachments/assets/79c6d0f5-8756-4a19-8903-76b56706056c" />

链表的特性和数组的特性性能分析
<img width="984" height="400" alt="image" src="https://github.com/user-attachments/assets/e87ad824-6a44-45bd-8a3c-0e8d3fb331ec" />


## 203. Remove Linked List Elements
https://leetcode.com/problems/remove-linked-list-elements/description/

文章链接：https://programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV18B4y1s7R9

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        # 创建虚拟头部节点以简化删除过程
        dummy_head = ListNode(next = head)
        
        # 遍历列表并删除值为val的节点
        current = dummy_head
        while current.next:
            if current.next.val == val:
                current.next = current.next.next
            else:
                current = current.next
        
        return dummy_head.next
```

## 707. Design Linked List

https://leetcode.com/problems/design-linked-list/description/

文章链接：https://programmercarl.com/0707.%E8%AE%BE%E8%AE%A1%E9%93%BE%E8%A1%A8.html#%E6%80%9D%E8%B7%AF

视频链接：https://www.bilibili.com/video/BV1FU4y1X7WD/?vd_source=dfe4be3e1289aa3263c6243a52315d05
```python
# 定义链表节点结构体
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class MyLinkedList:
    # 初始化链表
    def __init__(self):
        self.dummy_head = ListNode() # 这里定义的头结点 是一个虚拟头结点，而不是真正的链表头结点
        self.size = 0
    # 获取到第index个节点数值，如果index是非法数值直接返回-1， 注意index是从0开始的，第0个节点就是头结点
    def get(self, index: int) -> int:
        if index < 0 or index >= self.size:
            return -1
        
        current = self.dummy_head.next
        for i in range(index):
            current = current.next
            
        return current.val
    # 在链表最前面插入一个节点，插入完成后，新插入的节点为链表的新的头结点
    def addAtHead(self, val: int) -> None:
        self.dummy_head.next = ListNode(val, self.dummy_head.next)
        self.size += 1
    # 在链表最后面添加一个节点
    def addAtTail(self, val: int) -> None:
        current = self.dummy_head
        while current.next:
            current = current.next
        current.next = ListNode(val)
        self.size += 1
    # 在第index个节点之前插入一个新节点，例如index为0，那么新插入的节点为链表的新头节点。
    # 如果index 等于链表的长度，则说明是新插入的节点为链表的尾结点
    # 如果index大于链表的长度，则返回空
    # 如果index小于0，则在头部插入节点
    def addAtIndex(self, index: int, val: int) -> None:
        if index < 0 or index > self.size:
            return
        
        current = self.dummy_head
        for i in range(index):
            current = current.next
        current.next = ListNode(val, current.next)
        self.size += 1
    # 删除第index个节点，如果index 大于等于链表的长度，直接return，注意index是从0开始的
    def deleteAtIndex(self, index: int) -> None:
        if index < 0 or index >= self.size:
            return
        
        current = self.dummy_head
        for i in range(index):
            current = current.next
        current.next = current.next.next
        self.size -= 1
        


# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```


## 206. Reverse Linked List

https://leetcode.com/problems/reverse-linked-list/description/

文章链接：https://programmercarl.com/0206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1nB4y1i7eL/

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        curr = head
        while curr:
            nxt = curr.next # 保存一下cur的下一个节点，因为接下来要改变cur.next
            curr.next = prev # 反转
            # 更新pre、cur指针
            prev = curr
            curr = nxt
        return prev
```

# 链表part02

## 24. Swap Nodes in Pairs

https://leetcode.com/problems/swap-nodes-in-pairs/description/

文章链接：https://programmercarl.com/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

视频链接：https://www.bilibili.com/video/BV1YT411g7br/?vd_source=dfe4be3e1289aa3263c6243a52315d05

<img width="1456" height="456" alt="image" src="https://github.com/user-attachments/assets/687ac4b4-e7b8-4f1c-9a05-704f6a2974d8" />

<img width="1442" height="462" alt="image" src="https://github.com/user-attachments/assets/7f45ae00-fb09-44a6-b3a0-f6902a0bcb76" />

<img width="1588" height="346" alt="image" src="https://github.com/user-attachments/assets/d52edba2-5833-4314-a46f-052e005e6be9" />

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy_head = ListNode(next=head)
        current = dummy_head
        
        # 必须有cur的下一个和下下个才能交换，否则说明已经交换结束了
        while current.next and current.next.next:
            temp = current.next # 防止节点修改 1
            temp1 = current.next.next.next # 3
            
            current.next = current.next.next # 步骤一：cur->2
            current.next.next = temp # 步骤二：2->1
            temp.next = temp1 # 步骤三：1->3
            # 更新curr
            current = current.next.next # curr = 1
        return dummy_head.next
```
