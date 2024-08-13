
# LeetCode Interviewer

> # 🚩此项目决定不再维护，将其合并到了另一个项目 [NLP Learning Workshop](https://github.com/liu673/NLP-Learning-Workshop/tree/main)中，详细内容可跳转看呦！

## 📚项目简介
欢迎来到 LeetCode Interviewer，这是一个我专为面试准备的算法学习资源库，也希望自己能“学而时习之，思而时想之。”
该项目汇集并解析LeetCode上与面试紧密相关的经典算法题目，帮助有需要的同学高效备战技术面试。

希望读到这份文档的同学，能够快速掌握面试中常见的算法，迎接面对技术面试的挑战，开启职业生涯的新篇章！

## 📖目录
- [项目简介](#项目简介)
- [快速开始](#快速开始)
- [数组](#数组)
  - [二分查找](#二分查找)
  - [移除元素](#移除元素)
  - [长度最小的子数组](#长度最小的子数组)
  - 正在学习添加中...
- [链表](#链表)
- [哈希表](#哈希表)
- [字符串](#字符串)
- [致谢](#致谢)

## 🚀快速开始
1. 克隆项目
   ```shell
   git clone https://github.com/liu673/LeetCode_Interviewer.git
   ```

2. 选择题目

   - 浏览目录，根据自己的薄弱点或兴趣选择题目开始学习。
   - 因为内容过多，阅读时可以点击 ▶ 按钮查看题目详情。

3. 阅读与实践

   - 深入理解题目描述与示例。
   - 分析解题思路，理解每一步的逻辑。
   - 实现代码并提交到LeetCode验证。


## 数组
### 二分查找
<details>

[//]: # (<summary>二分查找</summary>)

[二分查找【LeetCode链接】](https://leetcode.cn/problems/binary-search/)
```text
给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

示例 1:
输入: nums = [-1,0,3,5,9,12], target = 9     
输出: 4       
解释: 9 出现在 nums 中并且下标为 4     

示例 2:
输入: nums = [-1,0,3,5,9,12], target = 2     
输出: -1        
解释: 2 不存在 nums 中因此返回 -1        
```
```python
"解法一：左闭右闭"
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1  # 定义target在左闭右闭的区间里，[left, right]

        while left <= right:
            middle = left + (right - left) // 2
            
            if nums[middle] > target:
                right = middle - 1  # target在左区间，所以[left, middle - 1]
            elif nums[middle] < target:
                left = middle + 1  # target在右区间，所以[middle + 1, right]
            else:
                return middle  # 数组中找到目标值，直接返回下标
        return -1  # 未找到目标值

"解法二：左闭右开"
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums)  # 定义target在左闭右开的区间里，即：[left, right)

        while left < right:  # 因为left == right的时候，在[left, right)是无效的空间，所以使用 <
            middle = left + (right - left) // 2

            if nums[middle] > target:
                right = middle  # target 在左区间，在[left, middle)中
            elif nums[middle] < target:
                left = middle + 1  # target 在右区间，在[middle + 1, right)中
            else:
                return middle  # 数组中找到目标值，直接返回下标
        return -1  # 未找到目标值
```
</details>

<details>
<summary>相关题目</summary>

1. 
   <details>
   <summary>搜索插入位置</summary>

   [搜索插入位置【LeetCode链接】](https://leetcode.cn/problems/search-insert-position/)
   
   ```text
   给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。
   
   请必须使用时间复杂度为 O(log n) 的算法。
 
   示例 1:
   输入: nums = [1,3,5,6], target = 5
   输出: 2
   
   示例 2:
   输入: nums = [1,3,5,6], target = 2
   输出: 1
   
   示例 3:   
   输入: nums = [1,3,5,6], target = 7
   输出: 4
   ```
   ```python
   class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        # 同样参考二分查找，左闭右闭与左闭右开
        left, right = 0, len(nums) - 1
        while left <= right:
            middle = left + (right - left) // 2
            if nums[middle] > target:
                right = middle - 1
            elif nums[middle] < target:
                left = middle + 1
            else:
                return nums.index(target)
        return right + 1
   ```
   </details>

2. 
   <details>
   <summary>在排序数组中查找元素的第一个和最后一个位置</summary>

   [在排序数组中查找元素的第一个和最后一个位置【LeetCode链接】](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/description/)
   
   ```text
   给你一个按照非递减顺序排列的整数数组 nums，和一个目标值 target。请你找出给定目标值在数组中的开始位置和结束位置。
   
   如果数组中不存在目标值 target，返回 [-1, -1]。
   
   你必须设计并实现时间复杂度为 O(log n) 的算法解决此问题。
   
   示例 1：
   输入：nums = [5,7,7,8,8,10], target = 8
   输出：[3,4]
   
   示例 2：
   输入：nums = [5,7,7,8,8,10], target = 6
   输出：[-1,-1]
   
   示例 3：   
   输入：nums = [], target = 0
   输出：[-1,-1]
   ```
   ```python
   class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        """解法一"""
        # def get_rightborder(nums, target):
        #     left, right = 0, len(nums) -1
        #     rightborder = -3
        #     while left <= right:
        #         middle = left + (right - left) // 2
        #         if nums[middle] > target:
        #             right = middle - 1
                    
        #         else:
        #             left = middle + 1
        #             rightborder = left
        #     return rightborder

        # def get_leftborder(nums, target):
        #     left, right = 0, len(nums) -1
        #     leftborder = -3
        #     while left <= right:
        #         middle = left + (right - left) // 2
        #         if nums[middle] >= target:
        #             right = middle - 1
        #             leftborder = right
        #         else:
        #             left = middle + 1
        #     return leftborder
        
        # leftborder = get_leftborder(nums, target)
        # rightborder = get_rightborder(nums, target)
        # # print(leftborder, rightborder)

        # if leftborder == -3 or rightborder == -3:
        #     return [-1, -1]
        # if rightborder - leftborder > 1:
        #     return [leftborder+1, rightborder-1]
        # else:
        #     return [-1, -1]

        """解法二"""
        def binarysearch(nums, target):
            left, right = 0, len(nums) - 1
            while left <= right:
                middle = left + (right - left) // 2
                if nums[middle] > target:
                    right = middle - 1
                elif nums[middle] < target:
                    left = middle + 1
                else:
                    return middle
            return -1
        
        index = binarysearch(nums, target)

        left, right = index, index

        if index == -1:
            return [-1, -1]
        while left - 1 >= 0 and nums[left - 1] == target:
            left -= 1
        while right + 1 < len(nums) and nums[right + 1] == target:
            right += 1
        return [left, right]
   ```
   </details>
3. 
    <details>
    <summary>x的平方根</summary>

    [x的平方根【LeetCode链接】](https://leetcode.cn/problems/sqrtx/description/)

    ```text
   给你一个非负整数 x ，计算并返回 x 的 算术平方根 。

   由于返回类型是整数，结果只保留 整数部分 ，小数部分将被 舍去 。
   
   注意：不允许使用任何内置指数函数和算符，例如 pow(x, 0.5) 或者 x ** 0.5 。
   
   示例 1：   
   输入：x = 4
   输出：2
   
   示例 2：
   输入：x = 8
   输出：2
   解释：8 的算术平方根是 2.82842..., 由于返回类型是整数，小数部分将被舍去。
    ```
    ```python
   class Solution:
    def mySqrt(self, x: int) -> int:
        left, right = 0, x
        while left <= right:
            middle = left + (right - left) // 2
            if middle * middle <= x:
                left = middle + 1
            else:
                right = middle - 1
        return left - 1
    ```
    </details>

4. 
    <details>
    <summary>有效的完全平方数</summary>

    [有效的完全平方数【LeetCode](https://leetcode.cn/problems/valid-perfect-square/description/)

    ```text
   给你一个正整数 num 。如果 num 是一个完全平方数，则返回 true ，否则返回 false 。

   完全平方数 是一个可以写成某个整数的平方的整数。换句话说，它可以写成某个整数和自身的乘积。
   
   不能使用任何内置的库函数，如  sqrt 。
   
   示例 1：   
   输入：num = 16
   输出：true
   解释：返回 true ，因为 4 * 4 = 16 且 4 是一个整数。
   
   示例 2：   
   输入：num = 14
   输出：false
   解释：返回 false ，因为 3.742 * 3.742 = 14 但 3.742 不是一个整数。
    ```
    ```python
   class Solution:
    def isPerfectSquare(self, num: int) -> bool:
        left, right = 0, num
        # while left <= right:
        #     middle = left + (right - left) // 2
        #     if middle * middle <= num:
        #         left = middle + 1
        #     else:
        #         right = middle - 1
        # result = left - 1
        # if result * result == num:
        #     return True
        # else:
        #     return False

        while left <= right:
            middle = (left + right) // 2
            if middle * middle == num:
                return True
            elif middle * middle <= num:
                left = middle + 1
            else:
                right = middle - 1
        return False
    ```
    </details>

</details>

### 移除元素
<details>

[移除元素【LeetCode链接】](https://leetcode.cn/problems/remove-element/description/)
```text
给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素。元素的顺序可能发生改变。然后返回 nums 中与 val 不同的元素的数量。

假设 nums 中不等于 val 的元素数量为 k，要通过此题，您需要执行以下操作：
- 更改 nums 数组，使 nums 的前 k 个元素包含不等于 val 的元素。nums 的其余元素和 nums 的大小并不重要。
- 返回 k。

示例 1：
输入：nums = [3,2,2,3], val = 3
输出：2, nums = [2,2,_,_]
解释：你的函数函数应该返回 k = 2, 并且 nums 中的前两个元素均为 2。
你在返回的 k 个元素之外留下了什么并不重要（因此它们并不计入评测）。

示例 2：
输入：nums = [0,1,2,2,3,0,4,2], val = 2
输出：5, nums = [0,1,4,0,3,_,_,_]
解释：你的函数应该返回 k = 5，并且 nums 中的前五个元素为 0,0,1,3,4。
注意这五个元素可以任意顺序返回。
你在返回的 k 个元素之外留下了什么并不重要（因此它们并不计入评测）。
```

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        "解法一：删除"
        # return len([i for i in nums if i !=val])
        # for i in range(len(nums)):
        #     if val in nums:
        #         del nums[nums.index(val)]
        # return len(nums)
        "解法二：快慢指针"
        # lower, fast = 0, 0
        # size = len(nums)
        # while fast < size:
        #     if nums[fast] != val:
        #         nums[lower] = nums[fast]
        #         lower += 1
        #     fast += 1
        # return lower
        "解法三：双向指针"
        left, right = 0, len(nums) - 1
        while left <= right:
            while left <= right and nums[left] != val:
                left += 1
            while left <= right and nums[right] == val:
                right -= 1
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        return left
```

</details>

<details>
<summary>相关题目</summary>

1. 
    <details>
    <summary>删除有序数组中的重复项</summary>

    [删除有序数组中的重复项【LeetCode链接】](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/description/)

    ```text
   给你一个 非严格递增排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 。然后返回 nums 中唯一元素的个数。

   考虑 nums 的唯一元素的数量为 k ，你需要做以下事情确保你的题解可以被通过：
   
   - 更改数组 nums ，使 nums 的前 k 个元素包含唯一元素，并按照它们最初在 nums 中出现的顺序排列。nums 的其余元素与 nums 的大小不重要。
   - 返回 k 。
   
   示例 1：
   输入：nums = [1,1,2]
   输出：2, nums = [1,2,_]
   解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。
   
   示例 2：
   输入：nums = [0,0,1,1,1,2,2,3,3,4]
   输出：5, nums = [0,1,2,3,4]
   解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。
    ```
    ```python
     class Solution:
        def removeDuplicates(self, nums: List[int]) -> int:
            # for i in nums:
            #     for ii in nums[nums.index(i)+1:]:
            #         if i == ii:
            #             del nums[nums.index(i)]
            # return len(nums)
    
            lower, fast = 0, 0
            size = len(nums)
            while fast < size:
                if nums[lower] == nums[fast]:
                    fast += 1
                else:
                    lower += 1
                    nums[lower] = nums[fast]
                    fast += 1
            return lower+1
    
            # left = 0
            # for right in range(1, len(nums)):
            #     if nums[left] != nums[right]:
            #         left += 1
            #         nums[left] = nums[right]
            #         right += 1
            #     right += 1
            # return left + 1
    
    ```
    </details>
   
2. 
    <details>
    <summary>移动零</summary>
    
    [移动零【LeetCode链接】](https://leetcode.cn/problems/move-zeroes/description/)
    ```text
   给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
   
   请注意 ，必须在不复制数组的情况下原地对数组进行操作。
   
   示例 1:
   输入: nums = [0,1,0,3,12]
   输出: [1,3,12,0,0]
   
   示例 2:
   输入: nums = [0]
   输出: [0]
    ```
    ```python
    class Solution:
        def moveZeroes(self, nums: List[int]) -> None:
            """
            Do not return anything, modify nums in-place instead.
            """
            lower, fast = 0, 0
            while fast < len(nums):
                if nums[fast] != 0:
                    nums[lower], nums[fast] = nums[fast], nums[lower]
                    lower += 1
                fast += 1
    
    ```
    
    </details>

3.
    <details>
    <summary>比较含退格的字符串</summary>
   
    [比较含退格的字符串【LeetCode链接】](https://leetcode.cn/problems/backspace-string-compare/)
    ```text
   给定 s 和 t 两个字符串，当它们分别被输入到空白的文本编辑器后，如果两者相等，返回 true 。# 代表退格字符。

   注意：如果对空文本输入退格字符，文本继续为空。
   
   示例 1：
   输入：s = "ab#c", t = "ad#c"
   输出：true
   解释：s 和 t 都会变成 "ac"。
   
   示例 2：
   输入：s = "ab##", t = "c#d#"
   输出：true
   解释：s 和 t 都会变成 ""。
   
   示例 3：
   输入：s = "a#c", t = "b"
   输出：false
   解释：s 会变成 "c"，但 t 仍然是 "b"。
    ```
    ```python
    class Solution:
        def backspaceCompare(self, s: str, t: str) -> bool:
    
            def str_info(st):
                res = ""
                for i in range(len(st)):
                    if st[i] != "#":
                        res += st[i]
                    else:
                        res = res[:-1]
                return res
    
            sort_s = str_info(s)
            sort_t = str_info(t)
    
            return sort_s == sort_t
    ```
    </details>

4. 
   <details>
   <summary>有序数组的平方</summary>

   [有序数组的平方【LeetCode链接】](https://leetcode.cn/problems/squares-of-a-sorted-array/description/)
   ```text
   给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。
   
   示例 1：
   输入：nums = [-4,-1,0,3,10]
   输出：[0,1,9,16,100]
   解释：平方后，数组变为 [16,1,0,9,100]
   排序后，数组变为 [0,1,9,16,100]
   
   示例 2：
   输入：nums = [-7,-3,2,3,11]
   输出：[4,9,9,49,121]
   ```
   ```python
   class Solution:
        def sortedSquares(self, nums: List[int]) -> List[int]:
            # return sorted([i * i for i in nums])

            left, right = 0, len(nums) -1
            res = [-1] * len(nums)   # 初识化存储结果
            site = len(nums) - 1     # 状态
            while left <= right:
                if nums[left] * nums[left] < nums[right] * nums[right]:
                    res[site] = nums[right] * nums[right]
                    right -= 1
                else:
                    res[site] = nums[left] * nums[left]
                    left += 1
                site -= 1
            return res

   ```
   </details>

</details>

### 长度最小的子数组
<details>

[长度最小的子数组【LeetCode链接】](https://leetcode.cn/problems/minimum-size-subarray-sum/description/)
```text
给定一个含有 n 个正整数的数组和一个正整数 target 。
找出该数组中满足其总和大于等于 target 的长度最小的 连续
子数组`[numsl, numsl+1, ..., numsr-1, numsr]`，并返回其长度。如果不存在符合条件的子数组，返回 0 。

示例 1：
输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。

示例 2：
输入：target = 4, nums = [1,4,4]
输出：1

示例 3：
输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0
```
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        l = len(nums)
        left = 0
        right = 0
        min_len = float('inf')
        cur_sum = 0  # 当前的累加值

        while right < l:
            cur_sum += nums[right]

            while cur_sum >= target:  # 当前累加值大于目标值
                min_len = min(min_len, right - left + 1)  # 更新最短子数组的长度
                # 从当前累加值cur_sum中减去nums[left]，并向右移动左指针left，缩小子数组的范围
                cur_sum -= nums[left]
                left += 1

            right += 1

        # print(nums[left - 1:right])
        return min_len if min_len != float('inf') else 0
```

</details>


<details>
<summary>相关题目</summary>

1. 
   <details>
   <summary>最小覆盖子串</summary>

   [最小覆盖子串【LeetCode链接】](https://leetcode.cn/problems/minimum-window-substring/description/)
   ```text
   给你一个字符串 s 、一个字符串 t 。返回 s 中涵盖 t 所有字符的最小子串。如果 s 中不存在涵盖 t 所有字符的子串，则返回空字符串 "" 。
   注意：
   - 对于 t 中重复字符，我们寻找的子字符串中该字符数量必须不少于 t 中该字符数量。
   - 如果 s 中存在这样的子串，我们保证它是唯一的答案。
   
   示例 1：
   输入：s = "ADOBECODEBANC", t = "ABC"
   输出："BANC"
   解释：最小覆盖子串 "BANC" 包含来自字符串 t 的 'A'、'B' 和 'C'。
   
   示例 2：
   输入：s = "a", t = "a"
   输出："a"
   解释：整个字符串 s 是最小覆盖子串。
   
   示例 3:
   输入: s = "a", t = "aa"
   输出: ""
   解释: t 中两个字符 'a' 均应包含在 s 的子串中，
   因此没有符合条件的子字符串，返回空字符串。
   ```
   ```python
   class Solution:
    def minWindow(self, s: str, t: str) -> str:
        counts = Counter(t)     # 统计字符串t和滑动窗口维护的子串的字符数量差值，初始为t字符串的字符数量
        diff = len(counts)      # 滑动窗口中缺失字符串t中字符的种类的数量，当diff为0，说明滑动窗口涵盖t中所有字符。初始为t中的所有不同字符数。
        m = len(s)
        left = 0            # 滑动窗口左边界
        right = 0           # 滑动窗口右边界，指向下一个要加入滑动窗口的字符
        min_len = m + 1     # 最小子串长度，初始为整个字符串长度 + 1，表示一个不可能的值
        sub_str_start = -1  # 最小子串起点，最终要返回的是子串，通过start和minLen来确定子串范围
        while right <= m:
            # 还有缺失的字符
            if diff > 0:
                if right == m: break    # 没有可以加入的字符，退出
                ch = s[right]           # 获取右边界指向的字符，右边界右移一位
                right += 1
                counts[ch] = counts.get(ch, 0) - 1  # 右边界字符加入滑动窗口，该字符的差距值 - 1
                if counts[ch] == 0:
                    diff -= 1   # 如果这个字符数量为0，说明新加入的字符使得有一种字符的数量满足要求，差值diff减1
            else:
                # 没有缺失的字符，当前滑动窗口维护的子串即为一个满足条件的子串
                if right - left < min_len:
                    # 更新最小子串
                    min_len = right - left
                    sub_str_start = left
                ch = s[left]        # 获取左边界指向的字符，左边界右移一位；尝试获取更短的子串
                left += 1
                counts[ch] = counts.get(ch, 0) + 1  # 左边界字符移出滑动窗口，该字符的差距值 + 1
                if counts[ch] == 1:
                    diff += 1       # 如果这个字符数量为1，说明原本为0，移除的字符使得有一种字符的数量欠缺了，因此差值diff加1
        # minLen仍为m+1，说明不存在涵盖t所有字符的子串，返回空字符串；否则提取找到的子串[subStrStart, subStrStart + minLen)
        return "" if min_len == m + 1 else s[sub_str_start: sub_str_start + min_len]
   ```
   
   </details>
2. 
   <details>
   <summary>水果成篮</summary>

   [水果成篮【LeetCode链接】](https://leetcode.cn/problems/fruit-into-baskets/description/)
   ```text
   你正在探访一家农场，农场从左到右种植了一排果树。这些树用一个整数数组 fruits 表示，其中 fruits[i] 是第 i 棵树上的水果 种类 。

   你想要尽可能多地收集水果。然而，农场的主人设定了一些严格的规矩，你必须按照要求采摘水果：
   
   你只有 两个 篮子，并且每个篮子只能装 单一类型 的水果。每个篮子能够装的水果总量没有限制。
   你可以选择任意一棵树开始采摘，你必须从 每棵 树（包括开始采摘的树）上 恰好摘一个水果 。采摘的水果应当符合篮子中的水果类型。每采摘一次，你将会向右移动到下一棵树，并继续采摘。
   一旦你走到某棵树前，但水果不符合篮子的水果类型，那么就必须停止采摘。
   给你一个整数数组 fruits ，返回你可以收集的水果的 最大 数目。
   
   示例 1：
   输入：fruits = [1,2,1]
   输出：3
   解释：可以采摘全部 3 棵树。
   
   示例 2：
   输入：fruits = [0,1,2,2]
   输出：3
   解释：可以采摘 [1,2,2] 这三棵树。
   如果从第一棵树开始采摘，则只能采摘 [0,1] 这两棵树。
   
   示例 3：
   输入：fruits = [1,2,3,2,2]
   输出：4
   解释：可以采摘 [2,3,2,2] 这四棵树。
   如果从第一棵树开始采摘，则只能采摘 [1,2] 这两棵树。
   
   示例 4：
   输入：fruits = [3,3,3,1,2,1,1,2,3,3,4]
   输出：5
   解释：可以采摘 [1,2,1,1,2] 这五棵树。
   ```
   ```python
   class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        l, r= 0, 0
        res = 0
        classdict = defaultdict(int)
        classcont = 0

        while r < len(fruits):
            if classdict[fruits[r]] == 0:
                classcont += 1
            classdict[fruits[r]] += 1

            while classcont >2:
                if classdict[fruits[l]] == 1:
                    classcont -= 1
                classdict[fruits[l]] -= 1
                l += 1
            
            res = max(res, r - l + 1)
            r += 1
        print(fruits[l: r])
        return res
   ```
   
   </details>
</details>

<details>
<summary>拓展延伸-解法</summary>

- [滑动窗口](https://leetcode.cn/problems/fruit-into-baskets/solutions/1437444/shen-du-jie-xi-zhe-dao-ti-he-by-linzeyin-6crr/)

</details>

## 链表

## 哈希表

## 字符串


## 💌致谢
感谢 [代码随想录](https://github.com/youngyangyang04/leetcode-master) 的开源整理，让我少走了很多弯路，同时帮助我理解了算法。
