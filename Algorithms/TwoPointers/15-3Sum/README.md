# 15. 3Sum (Java)

**题目链接：** [LeetCode 15 - 3Sum](https://leetcode.com/problems/3sum/)

---

## 💡 核心领悟 (Insights)
- **排序是前提**：为了高效使用双指针并方便“去重”，首先必须对数组进行升序排序。
- **降维打击**：三数之和 $a + b + c = 0$ 可以转化为：固定一个数 $a$，在剩下的数组中寻找两个数 $b + c = -a$。这样就把 $O(n^3)$ 的暴力搜索降级为 $O(n^2)$ 的双指针问题。
- **去重的艺术**：这道题最容易出错的地方是结果集重复。
  - **固定元素的去重**：如果当前固定的数与前一个相同，跳过。
  - **双指针的去重**：当找到一组解后，左右指针在收缩时，必须跳过所有相同的元素。
 
  - 📈 复杂度分析 (Complexity)时间复杂度: $O(n^2)$。排序 $O(n \log n)$，双指针遍历 $O(n^2)$。
  - 空间复杂度: $O(\log n)$ 或 $O(n)$，取决于排序算法的实现。📌 总结 (Summary)3Sum 是双指针算法的教科书级案例。
  - 它教会我们：面对高维搜索空间，通过排序和固定一个变量，可以极大地简化问题。 此外，它对代码实现的严密性要求很高，尤其是边界处的去重逻辑。
  - 超经典的 3Sum。思路大家都懂，但为什么总是过不了？关键就在**去重、去重、还是去重！** * **Tips**：排序后用双指针，就像在数组两头拉橡皮筋。记得找到解后要把重复的数字“一口气跳过去”，不然结果集里全是双胞胎～
  - Solving the 3Sum problem (LeetCode 15) is a journey from $O(n^3)$ to $O(n^2)$. By sorting the array and fixing one element, we transform a triple-nested search into a streamlined two-pointer approach. The real challenge? **Handling duplicates.** Efficient pruning and de-duplication are what separate a working solution from a high-performance one.

## 🚀 解题代码 (Sorting + Two Pointers)
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums); // 1. 排序
        
        for (int i = 0; i < nums.length - 2; i++) {
            if (nums[i] > 0) break; // 优化：如果第一个数就大于0，后面不可能相加为0
            if (i > 0 && nums[i] == nums[i - 1]) continue; // 2. 对固定元素a去重
            
            int left = i + 1, right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum < 0) {
                    left++;
                } else if (sum > 0) {
                    right--;
                } else {
                    ans.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    // 3. 找到解后，对b和c去重
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;
                    left++;
                    right--;
                }
            }
        }
        return ans;
    }
}
