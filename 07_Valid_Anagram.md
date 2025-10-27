https://leetcode.com/problems/valid-anagram/description/

https://neetcode.io/problems/is-anagram?list=neetcode150


**Description**
242. Valid Anagram
Solved
Easy
Topics
premium lock icon
Companies
Given two strings s and t, return true if t is an anagram of s, and false otherwise.

 

Example 1:

Input: s = "anagram", t = "nagaram"

Output: true

Example 2:

Input: s = "rat", t = "car"

Output: false

**C#**
```C#
public class Solution {
    public bool IsAnagram(string s, string t) {
        char[] cs = s.ToCharArray();
        char[] ct = t.ToCharArray();
        Array.Sort(cs);
        Array.Sort(ct);
        if(s.Length!=t.Length)
        {
            return false;
        }
        for(int i=0;i<=s.Length-1;i++)
        {
            if(cs[i] != ct[i])
            {
                return false;
            }
        }
        return true;
    }
}
```
**Python**
```Python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        ss = sorted(s)
        st = sorted(t)
        if len(s) != len(t):
            return False
        for i in range(len(s)):
            if(ss[i]!=st[i]):
                return False
        return True

```

**Better Solution**

**C#**

```C#
public class Solution {
    public bool IsAnagram(string s, string t) {
        int[] temp = new int[26];
        if(s.Length!=t.Length)
        {
            return false;
        }
        for(int i=0; i<=s.Length-1;i++)
        {
            temp[s[i]-'a']++;
            temp[t[i]-'a']--;
        }
        var result = temp.Any(x=>x!=0);
        return !result;
    }
}
```

**Python**

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        temp = [0] * 26
        for i in range(len(s)):
            temp[ord(s[i])-ord('a')]+=1;
            temp[ord(t[i])-ord('a')]-=1;
        for i in range(len(temp)):
            if temp[i] != 0:
                return False
        return True
```
