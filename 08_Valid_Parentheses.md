https://leetcode.com/problems/valid-parentheses/
https://neetcode.io/problems/validate-parentheses?list=neetcode150

**Valid Parentheses**

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.
 

Example 1:

Input: s = "()"

Output: true

Example 2:

Input: s = "()[]{}"

Output: true

Example 3:

Input: s = "(]"

Output: false

Example 4:

Input: s = "([])"

Output: true

Example 5:

Input: s = "([)]"

Output: false

 

Constraints:

1 <= s.length <= 104
s consists of parentheses only '()[]{}'.

**C#**
```C#
public class Solution {
    public bool IsValid(string s) 
    {    
        Dictionary<char,char> dict = new Dictionary<char,char>()
        {{'{','}'},{'(',')'},{'[',']'}};
        Stack<char> st = new Stack<char>();
        foreach(var i in s)
        {
            if(dict.ContainsKey(i))
            {
                st.Push(i);
            }
            else 
            {
                if(st.Count==0) return false;
                char popped = st.Pop();
                if(i != dict[popped])
                {
                    return false;
                }
            }
        }
            return st.Count==0;

    }
    
}

```

**Python**
```Python
class Solution:
    def isValid(self, s: str) -> bool:
        dict = {'{':'}','[':']','(':')'}
        stack = []
        for i in s:
            if i in dict:
                stack.append(i)
            else:
                if not stack or dict[stack.pop()] != i:
                    return False
        return not stack
```
