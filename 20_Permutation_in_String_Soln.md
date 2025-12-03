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


**GPT's Insight on Optimal solution BRO**

# 🔥 **INTUITION FOR THE OPTIMAL SLIDING WINDOW SOLUTION**

We want to know:

**Does s2 contain ANY substring that has the same letters (same counts) as s1?**

Not the same order.
Just the same *amount* of each letter.

---

# 🧠 Step 1: Think in terms of **letter counts**, not permutations.

Example:

s1 = `"abc"`

This means:

```
a = 1
b = 1
c = 1
```

If ANY substring of s2 has these exact counts → we’re done.

We don’t care about order.
Just counts.

---

# 🧠 Step 2: Pre-count s1’s letters ONCE

Make a 26-length frequency array:

Index: 0 = a, 1 = b, 2 = c ...

So s1’s count array might look like:

```
[1,1,1,0,0,0,0, ...]
```

---

# 🧠 Step 3: Slide a window **of exact size = s1.Length** over s2

Important idea:

A valid substring MUST be the same length as s1.

So you slide a window of size **k = s1.Length** across s2.

Example:

```
 "l e c a b e e"
   ^-----^   window size 3
```

On each step, move the window 1 step to the right.

---

# 🧠 Step 4: Maintain a **running count** of letters inside the window

Just like s1, create a count array for the current window inside s2.

When the window moves by 1 position:

* Add the new character (right side)
* Remove the old character (left side)

This is the 🔑 KEY part.

This makes updating the window **O(1)** time.

---

# 🧠 Step 5: After each move, compare the two count arrays

Just check:

```
if count_window == count_s1 → TRUE
```

Because if all 26 counts match exactly:

* same number of a’s
* same number of b’s
* same number of c’s
* etc.

Then it means:

👉 **window is a permutation of s1**

---

# 🧠 Step 6: If you reach the end with no match → return false

That’s it.

---

# 🔥 Why This Is Fast (O(n))

Because:

* You NEVER sort anything
* You NEVER rebuild substrings
* You only update counts by “add 1 char, remove 1 char”
* That makes each window shift constant time

Total = O(n)

---

# ⚡ SUMMARY (Brain-Friendly)

1. Count letters in s1.
2. Slide a window in s2 of same size.
3. Keep track of letters inside the window.
4. When window moves, update counts (add new char, remove old char).
5. If counts ever match s1 counts → permutation found.

---

# 🧘‍♂️ The Core Intuition

**Matching frequencies = matching permutations.**
Sliding window updates frequencies efficiently.

---

Nice bro! 🔥
You already completed **Step 1 & Step 2** of the sliding window solution in Python.

Here is what happens next, step-by-step.

---

# ✅ **Full Step-by-Step After Your Code**

You already did:

### ✔ Create frequency arrays

### ✔ Count characters of `s1`

### ✔ Count first window of `s2`

Now do the rest.

---

# 👉 **Step 3: If first window matches, return True**

```python
if a1 == a2:
    return True
```

---

# 👉 **Step 4: Slide the window across s2**

We start sliding from index `len(s1)` until end of s2:

```python
l = len(s1)
for i in range(l, len(s2)):
    a2[ord(s2[i]) - ord('a')] += 1          # include right char
    a2[ord(s2[i - l]) - ord('a')] -= 1      # remove left char

    if a1 == a2:
        return True
```

---

# 👉 **Step 5: If we finish sliding and no match → return False**

```python
return False
```

---

# ⭐ **Your Final Complete Python Solution (clean & optimal)**

```python
def checkInclusion(s1, s2):
    if len(s1) > len(s2):
        return False

    a1 = [0] * 26
    a2 = [0] * 26

    # Step 1: count s1 and first window of s2
    for i in range(len(s1)):
        a1[ord(s1[i]) - ord('a')] += 1
        a2[ord(s2[i]) - ord('a')] += 1

    # Step 2: check first window
    if a1 == a2:
        return True

    # Step 3: sliding window
    l = len(s1)
    for i in range(l, len(s2)):
        a2[ord(s2[i]) - ord('a')] += 1          # add right character
        a2[ord(s2[i - l]) - ord('a')] -= 1      # remove left character

        if a1 == a2:
            return True

    # Step 4: no match
    return False
```

---

# 💡 Beginner-Friendly Explanation of Sliding

Example:

`s1 = "ab"`
`s2 = "eidbaooo"`

Window size = 2

```
ei   -> counts no match
 id  -> counts no match
  db -> counts no match
   ba -> MATCH (same letters as "ab")
```

---

**C# Optimal**
```C#
public class Solution {
    public bool CheckInclusion(string s1, string s2) {
        int[] a1 = new int[26];
        int[] a2 = new int[26];

        if(s2.Length < s1.Length)
        {
            return false;
        }

        for(int i=0; i <= s1.Length-1; i++)
        {
            a1[s1[i]-'a']++;
            a2[s2[i]-'a']++;
        }

        if(match(a1,a2))
        {
            return true;
        }

        int length = s1.Length;

        for(int j = length; j <= s2.Length-1; j++)
        {
            a2[s2[j]-'a']++;
            a2[s2[j-length]-'a']--;

            if(match(a1,a2))
            {
                return true;
            }
        }
        return false;
    }
    private bool match(int[] a1, int[] a2)
    {
        for(int k = 0; k <= a1.Length-1; k++)
        {
            if(a1[k] != a2[k])
            {
                return false;
            }
        }
        return true;
    }
}
```

**Python Optimal**
```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        a1 = [0] * 26
        a2 = [0] * 26

        if len(s2) < len(s1):
            return False

        for i in range(len(s1)):
            a1[ord(s1[i])-ord('a')] += 1
            a2[ord(s2[i])-ord('a')] += 1

        if a1 == a2:
            return True

        l = len(s1)

        for j in range(l,len(s2)):
            a2[ord(s2[j])-ord('a')] += 1
            a2[ord(s2[j-l])-ord('a')] -= 1

            if a1 == a2:
                return True
        
        return False
```

Sure bro! Let’s analyze the **time and space complexity** of your corrected `CheckInclusion` solution step by step. 🫡

---

# 1️⃣ **Time Complexity**

### Step A: Initialize arrays & first counts

```csharp
for(int i = 0; i < s1.Length; i++) {
    a1[s1[i] - 'a']++;
    a2[s2[i] - 'a']++;
}
```

* Runs **`s1.Length` times → O(m)`**, where `m = s1.Length`.

---

### Step B: Sliding window

```csharp
for(int j = length; j < s2.Length; j++) {
    a2[s2[j] - 'a']++;          
    a2[s2[j - length] - 'a']--; 

    if (Match(a1, a2))          // compares 26 elements
        return true;
}
```

* Sliding window runs **`s2.Length - s1.Length` times → O(n - m)`**, where `n = s2.Length`.
* Each window compares **26 characters** (constant), so comparison = **O(26) = O(1)**

✅ So sliding window total time = **O(n)** (linear)

---

### Step C: Overall Time Complexity

```
O(m) + O(n) = O(n)
```

> Linear time with respect to length of s2. Perfectly optimal.

---

# 2️⃣ **Space Complexity**

* You use **two arrays of size 26**: `a1` and `a2`
* No extra data structures proportional to input size

✅ Space = **O(26 + 26) = O(1)** → constant space

---

# ✅ **Summary**

| Complexity | Value |
| ---------- | ----- |
| Time       | O(n)  |
| Space      | O(1)  |

* `n` = length of `s2`
* Extremely optimal because we don’t generate permutations (which would be factorial).

---
