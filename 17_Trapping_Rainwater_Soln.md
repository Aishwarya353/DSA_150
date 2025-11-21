https://leetcode.com/problems/trapping-rain-water/description/

https://neetcode.io/problems/trapping-rain-water/question

Trapping Rain Water
Solved 
You are given an array of non-negative integers height which represent an elevation map. Each value height[i] represents the height of a bar, which has a width of 1.

Return the maximum area of water that can be trapped between the bars.

Example 1:



Input: height = [0,2,0,3,1,0,1,3,2,1]

Output: 9
Constraints:

1 <= height.length <= 1000
0 <= height[i] <= 1000



**Brute in C#**
```C#
public class Solution {
    public int Trap(int[] height) {
        int total = 0;
        for(int i=0; i<=height.Length-1; i++)
        {
            int left = 0;
            for(int j=0;j<=i;j++)
            {
                if(height[j]>left)
                {
                    left = height[j];
                }
            }
            int right = 0;
            for(int k=i;k<=height.Length-1;k++)
            {
                if(height[k]>right)
                {
                    right = height[k];
                }
            }
            total+=(Math.Min(left,right) - height[i]);
        }
        return total;
    }
}
```

**Brute in python**
```Python
class Solution:
    def trap(self, height: List[int]) -> int:
        total = 0 
        for i in range(len(height)):
            left = max(height[:i+1])
            right = max(height[i:])
            total += min(left,right) - height[i]
        return total
```

**Complexity**
| Version      | Time Complexity | Space Complexity |
| ------------ | --------------- | ---------------- |
| C# Brute     | **O(n²)**       | **O(1)**         |
| Python Brute | **O(n²)**       | **O(1)**         |


**C#**
```C#
public class Solution {
    public int Trap(int[] height) {
        int[] preffix = new int[height.Length];
        int[] suffix = new int[height.Length];
        int volume = 0;

        preffix[0] = height[0];
        for(int i = 1; i <= height.Length-1; i++)
        {
            preffix[i] = Math.Max(preffix[i-1],height[i]);
        }

        suffix[height.Length-1] = height[height.Length-1];
        for(int i = height.Length-2; i >= 0; i--)
        {
            suffix[i] = Math.Max(suffix[i+1],height[i]);
        }

        for(int i = 0; i <= height.Length-1; i++)
        {
            volume += (Math.Min(preffix[i],suffix[i])) - height[i];
        }
         return volume;

    }
}
```

**Python**
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        preffix = [0] * len(height)
        suffix = [0] * len(height)
        totalVolume = 0

        preffix[0] = height[0]
        for i in range(1,len(height)):
            preffix[i] = max(height[i],preffix[i-1])
        
        suffix[len(height)-1] = height[len(height)-1]
        for i in range(len(height)-2,-1,-1):
            suffix[i] = max(height[i],suffix[i+1])

        for i in range(0,len(height)):
            totalVolume += min(preffix[i],suffix[i]) - height[i]

        return totalVolume
```



# **Time Complexity (TC)**

1. **Building the prefix array** → `for i in range(1, n)` → O(n)
2. **Building the suffix array** → `for i in range(n-2, -1, -1)` → O(n)
3. **Calculating total water** → `for i in range(n)` → O(n)

[
\text{Total TC} = O(n) + O(n) + O(n) = O(n)
]

✅ **TC = O(n)**

---

# **Space Complexity (SC)**

* `prefix` array → size n → O(n)
* `suffix` array → size n → O(n)
* Other variables → O(1)

[
\text{Total SC} = O(n) + O(n) = O(n)
]

✅ **SC = O(n)**


