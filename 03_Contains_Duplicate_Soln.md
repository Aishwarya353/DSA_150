https://leetcode.com/problems/contains-duplicate/description/

https://neetcode.io/problems/duplicate-integer?list=neetcode150

**Contains Duplicate**
Solved 
Given an integer array nums, return true if any value appears more than once in the array, otherwise return false.

Example 1:

Input: nums = [1, 2, 3, 3]

Output: true

Example 2:

Input: nums = [1, 2, 3, 4]

Output: false

----

**Pattern Used : Hashing**

----

**C#**

    public class Solution {
        public bool ContainsDuplicate(int[] nums) {
            Dictionary<int,int> dict = new Dictionary<int,int>();
            for(int i=0; i<=nums.Length-1; i++)
            {
                if(dict.ContainsKey(nums[i]))
                {
                    return true;
                }
                else
                {
                    dict[nums[i]] = 1;
                }
            }

**Python**

    class Solution:
        def containsDuplicate(self, nums: List[int]) -> bool:
            dicts = {}
            for i in nums:
                if i in dicts:
                    return True
                else:
                    dicts[i] = 1
            return False

----

**GPT's Insight**

### 💡 Problem Recap:

> You’re solving **“Contains Duplicate”**:
> Return `True` if any number appears **more than once** in the array.

---

## ✅ Your Current Approach

You're using a **hash map (dictionary)** to track seen elements.

* **Time:** `O(n)`
* **Space:** `O(n)`

➡️ This is **already optimal** in terms of **time**.

---

## 🧠 Can We Use Two Pointers?

Short answer: **Yes, but only after sorting.**

Here's how:

### ▶️ Two Pointers Approach (After Sorting)

1. **Sort the array** → `O(n log n)`
2. Use **two pointers** (`i` and `i+1`) to compare adjacent elements.
3. If you find `nums[i] == nums[i+1]`, return `True`.

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        nums.sort()  # O(n log n)
        for i in range(1, len(nums)):
            if nums[i] == nums[i - 1]:
                return True
        return False
```

---

## 📊 Complexity of This Approach:

| Metric | Value                                                                |
| ------ | -------------------------------------------------------------------- |
| Time   | **O(n log n)** (because of sorting)                                  |
| Space  | **O(1)** (if sorting in-place) or **O(n)** (if sorting makes a copy) |

---

## 🤔 So Which One Should You Use?

| Scenario                   | Best Approach                        |
| -------------------------- | ------------------------------------ |
| Need **fastest** execution | **Hashing** (O(n))                   |
| Need **least extra space** | **Sort + Two Pointers** (O(1) space) |

So:

* ✅ **Your current code (with dict)** is best for **speed**
* ✅ **Two pointers** is good when **space is limited** (e.g., embedded systems, memory-constrained environments)

        return false;
    }
}
