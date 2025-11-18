https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/

https://neetcode.io/problems/two-integer-sum-ii?list=neetcode150

Given an array of integers numbers that is sorted in non-decreasing order.

Return the indices (1-indexed) of two numbers, [index1, index2], such that they add up to a given target number target and index1 < index2. Note that index1 and index2 cannot be equal, therefore you may not use the same element twice.

There will always be exactly one valid solution.

Your solution must use 
O
(
1
)
O(1) additional space.

Example 1:

Input: numbers = [1,2,3,4], target = 3

Output: [1,2]
Explanation:
The sum of 1 and 2 is 3. Since we are assuming a 1-indexed array, index1 = 1, index2 = 2. We return [1, 2].

Constraints:

2 <= numbers.length <= 1000
-1000 <= numbers[i] <= 1000
-1000 <= target <= 1000

**C#**
```C#
public class Solution {
    public int[] TwoSum(int[] numbers, int target) {
        int i=0;
        int j=numbers.Length-1;
        while(i < j)
        {
            if(numbers[i]+numbers[j]<target)
            {
                i++;
            }
            else if(numbers[i]+numbers[j]>target)
            {
                j--;
            }
            else
            {
                return new int[] {i+1,j+1};
            }
        }
        return new int[] {-1,-1};
    }
}
```

**Python**
```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        i = 0
        j = len(numbers)-1
        while i < j:
            if(numbers[i] + numbers[j] < target):
                i+=1
            elif(numbers[i] + numbers[j] > target):
                j-=1
            else:
                return [i+1,j+1]
        return [-1,-1]
```
**Complexity**

Sure bro 😎 — here are the complexities:

# ✅ **Time Complexity (TC)**

### **O(n)**

Because:

* You start with two pointers (`i` at the start, `j` at the end)
* Each step either increments `i` or decrements `j`
* Each pointer moves at most **n** times

So total operations ≤ **n**
➡️ **TC = O(n)**

---

# ✅ **Space Complexity (SC)**

### **O(1)**

Because:

* You only use two integer variables (`i` and `j`)
* No extra arrays, no hash map

So constant space
➡️ **SC = O(1)**

---

# 🔥 Final Answer

✔ **Time Complexity: O(n)**
✔ **Space Complexity: O(1)**

| Method                       | Time       | Space    |
| ---------------------------- | ---------- | -------- |
| Two pointers (your solution) | **O(n)**   | **O(1)** |
| HashMap (not allowed)        | O(n)       | O(n)     |
| Binary search for each i     | O(n log n) | O(1)     |
| Brute force                  | O(n²)      | O(1)     |
