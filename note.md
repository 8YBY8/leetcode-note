# Two Pointers
**Need to make two pointers**

1. make a left pointer and right pointer:
   `l,r = 0, len(list) - 1`
2. move left pointer to right or move right pointer to left by one in different condition:
   `if ...: l += 1` and
   `if ...: r -= 1`
3. program ends with left pointer next to the right pointer

![Two Pointer Visualiation](twoPointers.jpg)

# Stack
**last in first out**

1. To make a stack: `stack = []`
2. Add a value:`stack.append(value)`. Add a pair `stack.append([index, value])`
3. Remove last value: `stack.pop()`



enumerate() means get the index and value at the same time

`pair: [temp, index]` To make a pair 

stack[-1] get the top of the stack


# Linked List

make a linker list: `ll = {}`
It has val and node

1. create slow and fast pointer: `slow, fast = head, head`
2. in the looping, update these by `slow = slow.next` and `fast = fast.next.next`
