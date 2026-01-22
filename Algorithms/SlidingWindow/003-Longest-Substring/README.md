# 3. Longest Substring Without Repeating Characters (Java)

**题目链接：** [LeetCode 3 - Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

---

## 💡 核心领悟 (Insights)
- **滑动窗口 (Sliding Window)**：想象一个可伸缩的“窗口”在字符串上滑动。`left` 是左边界，`right` 是右边界。
- **动态调整**：
  - 当遇到重复字符时，窗口左边界 `left` 必须向右收缩，直到窗口内不再包含该重复字符。
  - 窗口移动过程中，实时更新 `maxLen = Math.max(maxLen, right - left + 1)`。
- **两种优化方案**：
  1. **HashSet (基础版)**：通过移除元素来被动调整窗口。
  2. **HashMap (进阶版)**：直接记录字符位置，让 `left` 实现“瞬移”优化。

---

## 🚀 解题方案

### 方法一：使用 HashSet (经典滑动窗口)
**思路**：`right` 不断向右移，如果发现 `set` 中已存在，则 `left` 不断移除字符直到重复消失。



```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> set = new HashSet<>();
        int left = 0, maxLen = 0;
        for (int right = 0; right < s.length(); right++) {
            while (set.contains(s.charAt(right))) {
                set.remove(s.charAt(left));
                left++;
            }
            set.add(s.charAt(right));
            maxLen = Math.max(maxLen, right - left + 1);
        }
        return maxLen;
    }
}
```

### 方法二：使用 HashMap (优化索引版)
**思路**：用 Map<Character, Integer> 存储字符及其对应的最新索引。当遇到重复时，left 无需一步步移动，而是直接跳到 Math.max(left, map.get(char) + 1)。
```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int left = 0, maxLen = 0;
        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);
            if (map.containsKey(c)) {
                // 注意：left 只能向右跳，不能往回退
                left = Math.max(left, map.get(c) + 1);
            }
            map.put(c, right);
            maxLen = Math.max(maxLen, right - left + 1);
        }
        return maxLen;
    }
}
