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
