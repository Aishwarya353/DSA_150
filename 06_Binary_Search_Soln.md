https://leetcode.com/problems/binary-search/

https://neetcode.io/problems/binary-search?list=neetcode150

**Description**
Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.

Example 1:

Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
Example 2:

Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1

**Edge Case :** [5] and target = 5 // Note : we added left <= right instead of left < right
**Pattern :** Binary Search

**C# Solution**

    public class Solution {
        public int Search(int[] nums, int target) {
            int left = 0;
            int right = nums.Length-1;
            while(left <= right)
            {
                int mid = left + (right - left) / 2;
                if(nums[mid] == target)
                {
                    return mid;
                }
                if(nums[mid] < target)
                {
                    left = mid+1;
                }
                else if(nums[mid] > target)
                {
                    right = mid-1;
                }
            }
            return -1;
        }
    }

**Python Solution**

    class Solution:
        def search(self, nums: List[int], target: int) -> int:
            left = 0;
            right = len(nums)-1;
            while left <= right:
                mid = (left + right) // 2
                if nums[mid] == target: return mid
                elif nums[mid] < target: left = mid + 1
                else: right = mid - 1
            return -1

----

**Note:**

Great question! You're noticing a subtle difference in how the midpoint (`mid`) is calculated in **Python** vs **C#**:

---

## ✅ Short Answer:

* In **Python**, we usually write:

  ```python
  mid = (left + right) // 2
  ```
* In **C#**, we often write:

  ```csharp
  int mid = left + (right - left) / 2;
  ```

Both calculate the middle index for binary search, but the **C# version avoids integer overflow**, which is a potential risk in some languages. Let’s explain this in detail.

---

## 🧠 Why the Difference?

### ⚠️ 1. **Integer Overflow Concern in C-like Languages (e.g., C#, C++, Java):**

In C#, integers are fixed-size (typically 32-bit signed integers). If `left` and `right` are large enough, this:

```csharp
int mid = (left + right) / 2;
```

can cause **overflow**:

* For example: `left = 2_000_000_000`, `right = 2_000_000_000`
* `left + right = 4_000_000_000` → overflows max `int` (2,147,483,647)

✅ So to avoid this, use:

```csharp
int mid = left + (right - left) / 2;
```

This expression **cannot overflow**, because:

* `right - left` is safe (smaller range)
* `left + (safe number)` stays within bounds

---

### ✅ 2. **Why It’s Not Needed in Python**

Python integers are **arbitrary-precision** (they grow as needed), so:

```python
mid = (left + right) // 2
```

is safe, even if `left` and `right` are extremely large.

There’s **no risk of overflow** in Python.

---

### 📝 Summary:

| Expression                  | Language | Reason                               |
| --------------------------- | -------- | ------------------------------------ |
| `left + (right - left) / 2` | C#, Java | Avoids overflow in fixed-width `int` |
| `(left + right) // 2`       | Python   | No overflow risk due to big integers |

---

Ah — got it! You're asking a **math question** now:

> Why is this:

```csharp
mid = left + (right - left) / 2;
```

**mathematically the same as:**

```csharp
mid = (left + right) / 2;
```

Let’s **prove** they’re the same using **algebra**.

---

## 🧮 Let’s break it down:

We start with:

```csharp
mid = left + (right - left) / 2;
```

Let’s call `l = left`, `r = right`.

### So:

```
mid = l + (r - l) / 2
```

Now apply distributive property and simplify:

```
mid = l + r/2 - l/2
```

Combine like terms:

```
mid = (l - l/2) + r/2
mid = l*(1 - 1/2) + r/2
mid = l*(1/2) + r/2
```

Now:

```
mid = (l + r) / 2
```

✅ Proven: both expressions are **mathematically equivalent**.

---

## 🔁 In Words:

* `(left + right) / 2`: directly computes the average.
* `left + (right - left) / 2`: says, "Start at `left`, then go halfway toward `right`."

Same result, just rearranged to **avoid adding large numbers together** first.

---
