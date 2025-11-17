https://leetcode.com/problems/longest-consecutive-sequence/

https://neetcode.io/problems/longest-consecutive-sequence?list=neetcode150

Longest Consecutive Sequence
Solved 
Given an array of integers nums, return the length of the longest consecutive sequence of elements that can be formed.

A consecutive sequence is a sequence of elements in which each element is exactly 1 greater than the previous element. The elements do not have to be consecutive in the original array.

You must write an algorithm that runs in O(n) time.

Example 1:

Input: nums = [2,20,4,10,3,4,5]

Output: 4
Explanation: The longest consecutive sequence is [2, 3, 4, 5].

Example 2:

Input: nums = [0,3,2,5,4,6,1,1]

Output: 7
Constraints:

0 <= nums.length <= 1000
-10^9 <= nums[i] <= 10^9


**C#**
```C#
public class Solution {
    public int LongestConsecutive(int[] nums) {
        int max = 0;

        if(nums.Length==0 || nums==null)
        return 0;

        HashSet<int> mapp = new HashSet<int>(nums);

        foreach(int element in mapp)
        {
            if(!mapp.Contains(element-1))
            {
                int count = 1;
                int currentElement = element;
                while(mapp.Contains(currentElement+1)) 
                {
                    count++;
                    currentElement++;
                }
                max = (max>count)?max:count;
            }
        }
        return max;
    }
    
}
```

**Python**
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        if not nums:
            return 0

        sett = set(nums)
        maxResult = 0

        for i in sett:
            if i-1 not in sett:
                count = 1
                currentElement = i
                while currentElement+1 in sett:
                    count+=1
                    currentElement+=1
                maxResult = max(count,maxResult)
        return maxResult
```

**GPT's Insight**
Here are the **Time Complexity (TC)** and **Space Complexity (SC)** for the final working solution:

---

# ✅ **Time Complexity (TC): O(n)**

Explanation:

1. **Building the hash set:**

   ```python
   sett = set(nums)
   ```

   This takes **O(n)** time.

2. **Iterating through the set:**

   ```python
   for i in sett:
   ```

   This is also **O(n)** iterations in the worst case.

3. **Counting consecutive sequences:**
   The inner `while` loop runs **only when a number is the start of a sequence**.
   Importantly, each number is visited **at most once** across all iterations of the `while` loop.

So although there is a nested loop, the total number of iterations is **linear**, giving:

### **Total: O(n)**

---

# ✅ **Space Complexity (SC): O(n)**

Explanation:

1. The hash set `sett` stores all elements from the input → **O(n)** space.
2. A few integer variables (`count`, `currentElement`, `maxResult`) → **O(1)** space.

### **Total: O(n)**

---

# 🧠 Final Answer

| Complexity           | Value    |
| -------------------- | -------- |
| **Time Complexity**  | **O(n)** |
| **Space Complexity** | **O(n)** |

---

Great question — this is the **most common confusion** about this problem.

Even though the code *looks* like it has a nested loop, the **total work done by the inner loop is still O(n)**, not O(n²).
Let’s break it down in a simple and intuitive way.

---

# ✅ **Why the Time Complexity is O(n) even with a nested loop**

The trick is:

## **➡️ Each number is processed by the inner `while` loop at most once.**

Let’s analyze:

```python
for i in sett:
    if i - 1 not in sett:      # Only start at the beginning of a sequence
        currentElement = i
        while currentElement + 1 in sett:
            currentElement += 1
```

---

# 🔍 **Key Point: The inner loop only runs when a number is the start of a sequence**

Example array:

```
[1, 2, 3, 4, 100, 101]
```

The inner loop runs:

* For `i = 1`: it checks 2, 3, 4 → 3 steps
* For `i = 2`: it does **NOT** run (because 1 exists)
* For `i = 3`: does NOT run
* For `i = 4`: does NOT run
* For `i = 100`: it checks 101 → 1 step
* For `i = 101`: does NOT run

Total work across all inner loops: **4 steps + 1 step = 5 steps**
This matches the size of the array: **n = 6**

---

# 🧠 **Master Insight: Every number is touched at most once inside the while loop**

The inner loop moves like this:

```
1 → 2 → 3 → 4
```

Once the algorithm “consumes” the streak, it never checks these numbers again inside a while loop.

So even though the loops are nested in structure, **they are not nested in work**.

This is called **amortized O(n)**.

---

# 📌 **Analogy**

Think of it like walking along a line of tiles:

* Outer loop: checks every tile, O(n)
* Inner loop: walks forward only when at the *start* of a path
* But once walked, you never walk those same tiles again

So total steps walked = **number of tiles (n)**.

---

# 🧮 **Formal Proof**

* Outer loop: runs `n` times
* Inner loop: runs **total** of `n` times across all elements

Therefore:

```
Total work = O(n) + O(n) = O(n)
```

Not O(n²).

---

# ✔ Final Answer

### **Time Complexity: O(n) because every number is visited at most once by the inner loop.**

---
