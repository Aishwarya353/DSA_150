https://leetcode.com/problems/group-anagrams/submissions/1825633123/

https://neetcode.io/problems/anagram-groups?list=neetcode150

Given an array of strings strs, group the anagrams together. You can return the answer in any order.

 

Example 1:

Input: strs = ["eat","tea","tan","ate","nat","bat"]

Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Explanation:

There is no string in strs that can be rearranged to form "bat".
The strings "nat" and "tan" are anagrams as they can be rearranged to form each other.
The strings "ate", "eat", and "tea" are anagrams as they can be rearranged to form each other.
Example 2:

Input: strs = [""]

Output: [[""]]

Example 3:

Input: strs = ["a"]

Output: [["a"]]

 

Constraints:

1 <= strs.length <= 104
0 <= strs[i].length <= 100
strs[i] consists of lowercase English letters.

**C#**
```C#
public class Solution {
    public IList<IList<string>> GroupAnagrams(string[] strs) {
        Dictionary<string,IList<string>> dict = new Dictionary<string,IList<string>>();
        for(int i = 0; i <= strs.Length-1; i++)
        {
            char[] temp = strs[i].ToCharArray();
            //var sorted = Array.Sort(temp); ⚠️ Issue: Array.Sort() returns void, so you can’t assign it to a variable.
            Array.Sort(temp);
            var sorted = new string(temp);
            if(dict.ContainsKey(sorted))
            {
                dict[sorted].Add(strs[i]);
            }
            else
            {
                dict[sorted] = new List<string>() {strs[i]};
            }
        }
        return dict.Values.ToList();
    }
}
```

**Python**
```Python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        groups = {}
        for i in range(len(strs)):
            sortedd = ''.join(sorted(strs[i]))
            if(sortedd in groups):
                groups[sortedd].append(strs[i])
            else:
                groups[sortedd] = [strs[i]]
        return list(groups.values())
```

**C#**
```C#
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        mapp = defaultdict(list)
        for i in strs:
            temp = [0] * 26
            for j in i:
                temp[ord(j)-ord('a')]+=1
            mapp[tuple(temp)].append(i)
        return list(mapp.values())
```

**Python**
```Python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        mapp = defaultdict(list)
        for i in strs:
            temp = [0] * 26
            for j in i:
                temp[ord(j)-ord('a')]+=1
            mapp[tuple(temp)].append(i)
        return list(mapp.values())
```

**Complexity**
| Approach                      | Time Complexity         | Space Complexity | Notes                                  |
| ----------------------------- | ----------------------- | ---------------- | -------------------------------------- |
| **Sorted-string**             | ( O(N⋅KlogK) ) | ( O(N⋅K) ) | Simpler, but slower due to sorting     |
| **Character-count (hashing)** | ( O(N⋅KlogK) )        | ( O(N⋅K) ) | Faster, avoids sorting, fixed alphabet |


**GPT's Insights**
Absolutely — let’s look **deeply** at these two lines: 👇

```python
mapp = defaultdict(list)
mapp[tuple(temp)].append(i)
```

They are the **core of how the anagrams get grouped**.

---

## 🔍 Line 1: `mapp = defaultdict(list)`

### What it does

This creates a **dictionary-like object** (`defaultdict`) where each new key **automatically starts with an empty list** as its value.

If you used a normal dictionary (`dict`), you’d have to do this:

```python
if key not in mapp:
    mapp[key] = []
mapp[key].append(i)
```

But with `defaultdict(list)`, Python does this for you automatically whenever a new key is accessed.

### Why it matters here

We’re grouping words (`strs`) that are **anagrams** — meaning they have the same letter counts.
Each unique pattern of letter counts becomes a key in `mapp`.
We want all words that share the same pattern to go into the **same list**.

So `defaultdict(list)` makes grouping easy and clean.

---

## 🔍 Line 2: `mapp[tuple(temp)].append(i)`

Let’s unpack it piece by piece.

### Step 1 — `temp`

`temp` is a **list of 26 integers**, one for each lowercase English letter.
It represents how many times each letter appears in the current word `i`.

Example:
If `i = "eat"`, then:

```python
temp = [1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0]
# positions correspond to a,b,c,...,z
# 1 'a', 1 'e', 1 't'
```

### Step 2 — `tuple(temp)`

Lists **cannot be used as dictionary keys** because they are *mutable* (they can change).
Tuples are *immutable* and *hashable*, so we convert the list to a tuple.

That makes `tuple(temp)` a valid, unique key representing the “anagram signature” of the word.

Example:

```python
tuple(temp)  # (1, 0, 0, 0, 1, 0, ..., 1, 0)
```

### Step 3 — `mapp[tuple(temp)].append(i)`

This says:

> “Go to the list stored under the key `tuple(temp)` in the dictionary, and append the current word `i` to that list.”

If this key doesn’t exist yet, `defaultdict(list)` automatically creates an empty list before appending.

Example walkthrough:

| Word  | `tuple(temp)` (key)     | Dictionary after appending               |
| ----- | ----------------------- | ---------------------------------------- |
| "eat" | (1,0,0,0,1,0,...,1,0)   | `{ (1,0,0,0,1,...,1,0): ["eat"] }`       |
| "tea" | same key as "eat"       | `{ (1,0,0,0,1,...,1,0): ["eat","tea"] }` |
| "tan" | (1,0,0,0,0,0,...,1,1,0) | adds a new key with ["tan"]              |

---

✅ **Summary**

| Line                          | What it does                                                        | Why it matters                             |
| ----------------------------- | ------------------------------------------------------------------- | ------------------------------------------ |
| `mapp = defaultdict(list)`    | Creates a dictionary where each missing key starts as an empty list | Simplifies grouping logic                  |
| `mapp[tuple(temp)].append(i)` | Uses the character frequency tuple as a key and appends the word    | Groups all anagrams together automatically |

So, those two lines together implement the **entire grouping mechanism**:
they automatically cluster words by their **letter frequency signature**.
