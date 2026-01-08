# 141. Linked List Cycle (Java)

**题目链接：** [LeetCode 141 - Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

---

## 💡 核心领悟 (Insights)
- **快慢指针 (Floyd's Tortoise and Hare)**：这是解决环形链表最经典的方案。
  - **慢指针 (slow)**：每次走一步。
  - **快指针 (fast)**：每次走两步。
- **物理隐喻**：想象两个人在操场跑步，如果操场是环形的，跑得快的人（兔子）一定会在某个时刻“套圈”并追上跑得慢的人（乌龟）。
- **边界思考**：为什么快指针每次走两步？因为这样快慢指针的相对速度是 1，在环内它们之间的距离每步缩小 1，最终一定会相遇而不会发生“跳过”的情况。

## 🚀 解题代码 (Code - Fast & Slow Pointers)
```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }
        
        ListNode slow = head;
        ListNode fast = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;          // 走 1 步
            fast = fast.next.next;     // 走 2 步
            
            if (slow == fast) {        // 相遇了，说明有环
                return true;
            }
        }
        
        return false;                  // 快指针走到头了，说明无环
    }
}

