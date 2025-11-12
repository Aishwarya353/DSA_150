https://neetcode.io/problems/string-encode-and-decode?list=neetcode150

Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

Please implement encode and decode

Example 1:

Input: ["neet","code","love","you"]

Output:["neet","code","love","you"]
Example 2:

Input: ["we","say",":","yes"]

Output: ["we","say",":","yes"]
Constraints:

0 <= strs.length < 100
0 <= strs[i].length < 200
strs[i] contains only UTF-8 characters.


**Mah stupid version**
public class Solution {

    public string Encode(IList<string> strs) {
        string result = string.Empty;
        foreach(var element in strs)
        {
            string temp = "@"+ element + "#";
            result += temp;
        }
        Console.WriteLine(result);
        return result;
    }

    public List<string> Decode(string s) {
        List<string> result= new List<string>();
        string[] temp = s.Split('#');
        foreach(var element in temp)
        {
            if(string.IsNullOrEmpty(element))
            {
                continue;
            }
            string t = element.Replace("@","");
            result.Add(t);
        }
        return result;
   }
}

**It fails for this**
Input:

["we","say",":","yes","!@#$%^&*()"]
stdout:

@we#@say#@:#@yes#@!@#$%^&*()#
Your Output:

["we","say",":","yes","!","$%^&*()"]
Expected output:

["we","say",":","yes","!@#$%^&*()"]

Note : Add number of characters in a string

**Brute in C#**
```C#
public class Solution {

    public string Encode(IList<string> strs) {
        StringBuilder st = new StringBuilder();
        foreach(var element in strs)
        {
            int length = element.Length;
            st.Append(length).Append('#').Append(element);
        }
        Console.WriteLine(st.ToString());
        return st.ToString();
    }

    public List<string> Decode(string s) {
        List<string> result= new List<string>();
        int i = 0;
        while(i < s.Length)
        {
            int j = i;
            while(s[j]!='#')
            {
                j++;
            }
            int length = int.Parse(s.Substring(i,j-i));
            string word = s.Substring(j+1,length);
            result.Add(word);
            i = j+1+length;
        }
        return result;
   }
}

```

**Brute in Python**
```python
class Solution:

    def encode(self, strs: List[str]) -> str:
        temp = ""
        for element in strs:
            temp = temp + str(len(element)) + '#' + element
        print(temp)
        return temp
    def decode(self, s: str) -> List[str]:
        result = []
        i = 0
        while i < len(s):
            j = i
            while s[j]!="#":
                j+=1
            length = int(s[i:j])
            word = s[j+1:j+1+length]
            result.append(word)
            i = j + 1 + length
        return result
```

Ahhh perfect bro 😎 — now that your code is correct, let’s carefully analyze the **time and space complexity** of your `Encode` and `Decode` methods.

We’ll go **step by step**.

---

## 1️⃣ Encode

```csharp
public string Encode(IList<string> strs) {
    StringBuilder st = new StringBuilder();
    foreach(var element in strs)
    {
        int length = element.Length;
        st.Append(length).Append('#').Append(element);
    }
    return st.ToString();
}
```

### **Time Complexity**

* Let `n` = number of strings in `strs`.
* Let `L` = total number of characters in all strings combined.

Step by step:

1. `element.Length` → O(1) per string.
2. `Append(length + '#' + element)` → appends **all characters of element** → O(length of element).

So total time = sum of lengths of all strings = **O(L)**.

✅ **Time Complexity:** **O(L)**

---

### **Space Complexity**

* You store everything in `StringBuilder`.

* Total characters = sum of lengths of all strings + extra characters for lengths and `#`.

* Extra chars for lengths and `#` is negligible compared to `L`.

✅ **Space Complexity:** **O(L)**

---

## 2️⃣ Decode

```csharp
public List<string> Decode(string s) {
    List<string> result= new List<string>();
    int i = 0;
    while(i < s.Length)
    {
        int j = i;
        while(s[j]!='#')
        {
            j++;
        }
        int length = int.Parse(s.Substring(i,j-i));
        string word = s.Substring(j+1,length);
        result.Add(word);
        i = j+1+length;
    }
    return result;
}
```

### **Time Complexity**

* Let `L` = length of encoded string `s`.
* `while(i < s.Length)` → moves pointer `i` through **entire string** exactly once.
* Inside loop:

1. `while(s[j] != '#')` → scans digits of length (usually very small, ≤ number of digits in length) → negligible.
2. `Substring(j+1, length)` → O(length) to copy substring.

* Since every character of `s` is **processed exactly once**, total = **O(L)**.

✅ **Time Complexity:** **O(L)**

---

### **Space Complexity**

* `List<string> result` → stores all decoded strings → **total length = sum of lengths of all original strings**.
* Temporary `Substring` copies → each copy O(length) → but overall sum = L.

✅ **Space Complexity:** **O(L)**

---

### ✅ Summary Table

| Method | Time Complexity | Space Complexity |
| ------ | --------------- | ---------------- |
| Encode | O(L)            | O(L)             |
| Decode | O(L)            | O(L)             |

> L = total number of characters in all strings (original or encoded)

---
