https://leetcode.com/problems/two-sum/submissions/1806511354/

https://neetcode.io/problems/two-integer-sum?list=neetcode150

**Description**

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]
Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]
 

Constraints:

2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
Only one valid answer exists.

**For Unsorted : Hashing
For Sorted : Two Pointer approach**

**If Unsorted**

**Python**

    class Solution:
        def twoSum(self, nums: List[int], target: int) -> List[int]:
            seen = {}
            for i in range(len(nums)):
                comp = target - nums[i];
                if comp in seen:
                    return [i,seen[comp]];
                seen[nums[i]] = i;
            return [-1,-1]

**C#**

    public class Solution {
        public int[] TwoSum(int[] nums, int target) 
        {
            Dictionary<int,int> dict = new Dictionary<int,int>();
            for(int i=0; i<=nums.Length-1; i++)
            {
                int compliment = target - nums[i];
                if(!dict.ContainsKey(compliment))
                {
                    dict[nums[i]] = i;
                }
                else
                {
                    return new int[] {i,dict[compliment]};
     
                }
            }
            return new int[] {-1,-1};
        }
    }


**If Sorted**
Make sure both positive and negative numbers are sorted

**C#**

    public class Solution {
        public int[] TwoSum(int[] nums, int target) {
            int left = 0;
            int right = nums.Length-1;
            while(left < right)
            {
                int sums = nums[left] + nums[right];
                if(sums < target)
                {
                    left = left + 1;
                }
                else if (sums > target)
                {
                    right = right -1;
                }
                else
                {
                    return new int[] {left,right};
                }
            }
            return new int[] {-1,-1};
        }
    }


**Python**

     class Solution:
         def twoSum(self, nums: List[int], target: int) -> List[int]:
             right = len(nums)-1
             left = 0
             while(left < right):
                 print("one",left)
                 print("two",right)
                 sums = nums[left] + nums[right]
                 if target <  sums:
                     print("if")
                     right = right - 1
                 elif target > sums:
                     print("elif")
                     left = left + 1
                 else:
                     print("else")
                     return [left,right]
             return [-1,-1]


---

**GPT's Insights**

## 🔍 Problem Recap: Two Sum

### Input:

* A list of integers `nums`
* A target integer `target`

### Output:

* Indices of **two numbers** that sum up to `target`
* Only **one valid pair exists**
* **Do not use the same element twice**

---

## ✅ When to Use What:

| Situation      | Approach     | Time | Space |
| -------------- | ------------ | ---- | ----- |
| Unsorted Input | Hash Map     | O(n) | O(n)  |
| Sorted Input   | Two Pointers | O(n) | O(1)  |

---

## 🧠 1. **Unsorted Input → Use Hash Map**

### 🔑 Key Insight:

* Store each number and its index in a hash map
* For every new number, check if its "pair" (target - num) was already seen
* Return indices when found

---

## 🧠 2. **Sorted Input → Use Two Pointers**

### 🔑 Key Insight:

* Move `left` and `right` toward each other
* If the current sum is **too small**, increase `left`
* If the sum is **too large**, decrease `right`
* If it's **perfect**, return the indices

---

## ⚠️ Common Mistakes to Watch Out For:

* 🔁 Starting `right = len(nums)` instead of `len(nums)-1`
* 🔄 Reversing `left` and `right` movement logic
* 🧠 Not checking if the input is **actually sorted** before using two pointers
* 😅 Forgetting to update hash map after checking in the hash map solution

✅ **Repeat this pattern** on a few more problems:

* [Two Sum II (LeetCode 167)](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) (sorted input)
* [3Sum](https://leetcode.com/problems/3sum/) (Two Pointers inside a loop)
* [4Sum](https://leetcode.com/problems/4sum/) (Advanced)

✅ Add this to your **DSA Pattern Notebook** under:

* Pattern: **Two Pointers**
* Sub-pattern: **Two Sum on sorted array**
* Key trick: Shrinking window from both ends
