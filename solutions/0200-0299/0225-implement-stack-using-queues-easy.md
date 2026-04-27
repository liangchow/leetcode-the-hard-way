---
description: >-
  Author: @wkw, @DongDong | https://leetcode.com/problems/implement-stack-using-queues
---

# 0225 - Implement Stack using Queues (Easy)

## Problem Link

https://leetcode.com/problems/implement-stack-using-queues

## Problem Statement

Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (`push`, `top`, `pop`, and `empty`).

Implement the `MyStack` class:

- `void push(int x)` Pushes element x to the top of the stack.
- `int pop()` Removes the element on the top of the stack and returns it.
- `int top()` Returns the element on the top of the stack.
- `boolean empty()` Returns `true` if the stack is empty, `false` otherwise.

**Notes:**

- You must use **only** standard operations of a queue, which means that only `push to back`, `peek/pop from front`, `size` and `is empty` operations are valid.
- Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use only a queue's standard operations.

**Example 1:**

```
Input
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 2, 2, false]

Explanation
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // return 2
myStack.pop(); // return 2
myStack.empty(); // return False
```

**Constraints:**

- `1 <= x <= 9`
- At most `100` calls will be made to `push`, `pop`, `top`, and `empty`.
- All the calls to `pop` and `top` are valid.

## Approach 1: 2 Queues

We can push all elements to one queue. For `pop` and `top` function, we move first $$n - 1$$ elements to another queue. What's left would be the top element. For `pop` function, we pop the top element as well and swap the queue.

<Tabs>
<TabItem value="cpp" label="C++">
<SolutionAuthor name="@wkw"/>

```cpp
class MyStack {
public:
    queue<int> q1, q2;
    MyStack() { }

    void push(int x) {
        q1.push(x);
    }

    int pop() {
        while (q1.size() > 1) {
            int x = q1.front();
            q1.pop();
            q2.push(x);
        }
        int res = q1.front();
        q1.pop();
        swap(q1, q2);
        return res;
    }

    int top() {
        while (q1.size() > 1) {
            int x = q1.front();
            q1.pop();
            q2.push(x);
        }
        return q1.front();
    }

    bool empty() {
        return q1.empty();
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
```

</TabItem>

<TabItem value="python" label="Python">
<SolutionAuthor name="@DongDong"/>

```python
class MyStack:

    def __init__(self):
        # Initilize two queues using deque(). q1 serves as the working queue.
        self.q1 = deque()
        self.q2 = deque()

    def push(self, x: int) -> None:
        self.q1.append(x)

    def pop(self) -> int:
        # While there is more than 1 element in q1, pop (from left) and append the popped element to q2. Swap q1 and q2, making q2 ready for the next operation.
        while len(self.q1) > 1:
            elem = self.q1.popleft()
            self.q2.append(elem)
        res = self.q1.popleft()
        self.q1, self.q2 = self.q2, self.q1
        return res

    def top(self) -> int:
        # Similar to pop() from above, except returning the first element from q1.
        while len(self.q1) > 1:
            elem = self.q1.popleft()
            self.q2.append(elem)
        return self.q1[0]

    def empty(self) -> bool:
        return len(self.q1) == 0


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```

</TabItem>
</Tabs>

## Approach 2: 1 Queue

For every push, we simply make the order backwards for `push` function. For `pop`() and `top()`, we can use `front()` to get the top element and return it.

<Tabs>
<TabItem value="cpp" label="C++">
<SolutionAuthor name="@wkw"/>

```cpp
class MyStack {
public:
    queue<int> q1;
    MyStack() { }

    void push(int x) {
        q1.push(x);
        for (int i = 1; i < q1.size(); i++) {
            q1.push(q1.front());
            q1.pop();
        }
    }

    int pop() {
        int x = q1.front(); q1.pop();
        return x;
    }

    int top() {
        return q1.front();
    }

    bool empty() {
        return q1.empty();
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
```

</TabItem>

<TabItem value="python" label="Python">
<SolutionAuthor name="@DongDong"/>

```python
class MyStack:

    def __init__(self):
        # Initialize using double-ended queue, deque()
        self.q = deque()

    def push(self, x: int) -> None:
        self.q.append(x)
        
    def pop(self) -> int:
        # Pop (from left) every element on the queue, except the last one, and append them to q itself. This would effectively shift the targeted element from last to the first place. Then, pop and return this element.
        for i in range(len(self.q) - 1):
            elem = self.q.popleft()
            self.q.append(elem)
        return self.q.popleft()

    def top(self) -> int:
        return self.q[-1]

    def empty(self) -> bool:
        return len(self.q) == 0

# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```

</TabItem>
</Tabs>
