# 232. Implement Queue using Stacks (Java)

**题目链接：** [LeetCode 232 - Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)

## 💡 核心领悟 (Insights)
- **栈的特性**：后进先出 (LIFO)。
- **队列特性**：先进先出 (FIFO)。
- **双栈转换**：通过两个栈（Input Stack & Output Stack）实现。
  - 只有当 Output Stack 为空时，才将 Input Stack 的所有元素“倒入”。
  - 这种“懒加载”处理方式保证了**均摊时间复杂度为 O(1)**。

## 🚀 解题代码 (Code)
```java
class MyQueue {

    private Deque<Integer> inStack;
    private Deque<Integer> outStack;

    public MyQueue() {
        inStack = new ArrayDeque<>();
        outStack = new ArrayDeque<>(); 
    }
    
    public void push(int x) {
        inStack.push(x);
    }
    
    public int pop() {
        shiftStackIfNeeded();
        return outStack.pop();
    }
    
    public int peek() {
        shiftStackIfNeeded();
        return outStack.peek();
    }
    
    public boolean empty() {
        return inStack.isEmpty() && outStack.isEmpty();
    }

    private void shiftStackIfNeeded() {
        if (outStack.isEmpty()) {
            while (!inStack.isEmpty()) {
                outStack.push(inStack.pop());
            }
        }
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
