# 33. Search in Rotated Sorted Array (Java)

**题目链接：** [LeetCode 33 - Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

---

## 💡 核心领悟 (Insights)
- **二分的本质**：二分查找不仅适用于完全有序的数组。其核心在于**“每次都能通过某种逻辑排除掉一半的搜索空间”**。即使数组经过旋转，它依然由两个局部有序的部分组成。
- **关键逻辑**：在旋转数组中，`mid` 节点会将数组分成两部分，其中**必定有一半是有序的**。
  - 如果 `nums[left] <= nums[mid]`：说明左半部分是有序的。
  - 否则：右半部分是有序的。
- **判断去向**：先确定哪一半有序，再判断 `target` 是否在该有序区间内，从而决定缩小哪一边的范围。

- Rethinking Binary Search: Beyond Sorted Arrays.
- Binary Search is often associated with sorted data, but LeetCode 33 (Search in Rotated Sorted Array) proves its power in partially sorted structures. By identifying which half is monotonically increasing, we can still eliminate half of the search space at each step. This is a great exercise in edge-case handling and logical branching.

## 🚀 解题代码 (Code - Binary Search)
```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            
            // 步骤 1：判断哪一半是有序的
            if (nums[left] <= nums[mid]) { 
                // 左半部分有序
                if (target >= nums[left] && target < nums[mid]) {
                    right = mid - 1; // target 在左侧区间
                } else {
                    left = mid + 1;  // target 在右侧
                }
            } else { 
                // 右半部分有序
                if (target > nums[mid] && target <= nums[right]) {
                    left = mid + 1;  // target 在右侧区间
                } else {
                    right = mid - 1; // target 在左侧
                }
            }
        }
        return -1;
    }
}
