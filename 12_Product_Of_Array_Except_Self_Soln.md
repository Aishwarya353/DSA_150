https://leetcode.com/problems/product-of-array-except-self/description/

https://neetcode.io/problems/products-of-array-discluding-self?list=neetcode150

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

 

Example 1:

Input: nums = [1,2,3,4]
Output: [24,12,8,6]
Example 2:

Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
 

Constraints:

2 <= nums.length <= 105
-30 <= nums[i] <= 30
The input is generated such that answer[i] is guaranteed to fit in a 32-bit integer.
 

Follow up: Can you solve the problem in O(1) extra space complexity? (The output array does not count as extra space for space complexity analysis.)


**C#**
```C#
public class Solution {
    public int[] ProductExceptSelf(int[] nums) {
        int[] result = new int[nums.Length];
        int prefix = 1;
        for(int i=0; i<=nums.Length-1; i++)
        {
            result[i] = prefix;
            prefix *= nums[i];
        }
        int suffix = 1;
        for(int j=nums.Length-1; j>=0; j--)
        {
            result[j] *= suffix;
            suffix *= nums[j];
        }
        return result;
    }
}
```

**Python**
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        result = [1] * len(nums)
        prefix = 1
        for i in range(len(nums)):
            result[i] = prefix
            prefix *= nums[i]
        suffix = 1
        for j in range(len(nums)-1,-1,-1):
            result[j] *= suffix
            suffix *= nums[j]
        return result
```


**GPT's Insight**
Let’s take the **classic example:**

```text
nums = [1, 2, 3, 4]
```

We’ll walk through every iteration of both loops and track:
👉 `result[i]`, `prefix`, and `suffix`.

---

## 🥇 Step 1: Prefix pass (left → right)

We fill `result[i]` with **product of all elements to the left**.

Before loop:

```
result = [?, ?, ?, ?]
prefix = 1
```

| i | nums[i] | result[i] (set to prefix) | prefix (after *= nums[i]) | result array after this step |
| - | ------- | ------------------------- | ------------------------- | ---------------------------- |
| 0 | 1       | 1                         | 1×1 = 1                   | [1, ?, ?, ?]                 |
| 1 | 2       | 1                         | 1×2 = 2                   | [1, 1, ?, ?]                 |
| 2 | 3       | 2                         | 2×3 = 6                   | [1, 1, 2, ?]                 |
| 3 | 4       | 6                         | 6×4 = 24                  | [1, 1, 2, 6]                 |

✅ After prefix loop:

```
result = [1, 1, 2, 6]
(prefix = 24, but we’re done using it)
```

Meaning so far:

* result[i] holds product of all **numbers before index i**.

---

## 🥈 Step 2: Suffix pass (right → left)

Now we multiply each result[i] by **product of all elements to the right**.

Before loop:

```
suffix = 1
result = [1, 1, 2, 6]
```

| j | nums[j] | result[j] *= suffix | suffix (after *= nums[j]) | result array after this step |
| - | ------- | ------------------- | ------------------------- | ---------------------------- |
| 3 | 4       | 6 × 1 = 6           | 1×4 = 4                   | [1, 1, 2, 6]                 |
| 2 | 3       | 2 × 4 = 8           | 4×3 = 12                  | [1, 1, 8, 6]                 |
| 1 | 2       | 1 × 12 = 12         | 12×2 = 24                 | [1, 12, 8, 6]                |
| 0 | 1       | 1 × 24 = 24         | 24×1 = 24                 | [24, 12, 8, 6]               |

✅ Final output:

```
result = [24, 12, 8, 6]
```

---

### 🧠 Conceptually

For each index:

```
result[i] = (product of all to the left) × (product of all to the right)
```

* Left pass builds the first part.
* Right pass builds the second part and multiplies it in.

---
