https://leetcode.com/problems/permutation-in-string/description/

https://neetcode.io/problems/permutation-string/question

Permutation in String
Solved 
You are given two strings s1 and s2.

Return true if s2 contains a permutation of s1, or false otherwise. That means if a permutation of s1 exists as a substring of s2, then return true.

Both strings only contain lowercase letters.

Example 1:

Input: s1 = "abc", s2 = "lecabee"

Output: true
Explanation: The substring "cab" is a permutation of "abc" and is present in "lecabee".

Example 2:

Input: s1 = "abc", s2 = "lecaabee"

Output: false
Constraints:

1 <= s1.length, s2.length <= 1000

**C#**
```C#
public class Solution {
    public bool CheckInclusion(string s1, string s2) {
        int length = s1.Length;
        char[] c1 = s1.ToCharArray();
        Array.Sort(c1);
        string sortedS1 = new string(c1);
        for(int left = 0; left <= s2.Length-length; left++)
        {
            string substring = s2.Substring(left,length);
            char[] c2 = substring.ToCharArray();
            Array.Sort(c2);
            string sortedS2 = new string(c2);
            if(sortedS1==sortedS2)
            {
                return true;
            }
        }
        return false;
    }
}
```

**Python Brute**
```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        k = len(s1)
        sortedS1 = sorted(s1)
        for left in range(0 ,len(s2)-k+1):
            window = s2[left:left+k]
            if sortedS1 == sorted(window):
                return True
        return False
```


**GPT's Insight**
Sure — here’s the **time and space complexity** of *your* approach (the one where you sort every window).

---

# ✅ **Your Approach**

```python
for left in range(0, len(s2) - k + 1):
    window = s2[left : left + k]
    if sorted(window) == sortedS1:
        return True
```

Where:

* `n = len(s2)`
* `k = len(s1)`

---

# ⏱ **Time Complexity**

### 1. Loop runs `(n - k + 1)` times

≈ **O(n)** iterations.

### 2. Inside loop:

* slicing `s2[left:left+k]` takes **O(k)**
* sorting the window takes **O(k log k)**

Sorting dominates the cost.

### Total time:

```
O(n * (k log k))
```

---

# 💾 **Space Complexity**

### Sorting uses a temporary array of size **k**:

```
O(k)
```

Also you stored:

* `sortedS1` → O(k)

Total space:

```
O(k)
```

---

# ⭐ Final Answer

| Complexity | Value              |
| ---------- | ------------------ |
| **Time**   | **O(n · k log k)** |
| **Space**  | **O(k)**           |

---

# 🎯 Compare with optimal approach:

Sliding window + frequency arrays:

```
Time:  O(n)
Space: O(1)  (26 letters)
```
