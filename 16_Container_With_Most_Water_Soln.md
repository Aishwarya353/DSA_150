https://leetcode.com/problems/container-with-most-water/description/

https://neetcode.io/problems/max-water-container/question?list=neetcode150

Container With Most Water
Solved 
You are given an integer array heights where heights[i] represents the height of the 
i
t
h
i 
th
  bar.

You may choose any two bars to form a container. Return the maximum amount of water a container can store.

Example 1:



Input: height = [1,7,2,5,4,7,3,6]

Output: 36
Example 2:

Input: height = [2,2,2]

Output: 4
Constraints:

2 <= height.length <= 1000
0 <= height[i] <= 1000


**GPT's Insight on understanding the question**
Absolutely, let’s break down the problem together!

### Problem Breakdown:

* You’re given an array of integers, `heights[]`, where each element represents the height of a bar in a graph.
* You need to pick two bars (elements) from this array, and the "container" formed between these two bars will store a certain amount of water.
* The container's capacity (or how much water it can hold) depends on two things:

  1. **The distance between the two bars**: The farther apart they are, the larger the base of the container.
  2. **The height of the shorter bar**: The height of water that the container can hold is limited by the shorter of the two bars because water will spill over the shorter one.

So, **the amount of water** a container can store is calculated as:
[
\text{Water} = \text{min(height1, height2)} \times \text{distance between the bars}
]
Where:

* `height1` is the height of the first bar.
* `height2` is the height of the second bar.
* The distance between the bars is just the difference in their indices (positions) in the array.

### What do you need to do?

You need to **find two bars** in the array such that they maximize the amount of water they can store.

### Example:

Consider the array of heights: `[1, 8, 6, 2, 5, 4, 8, 3, 7]`

* For bars at index `1` (height 8) and index `8` (height 7), the container's water capacity would be:
  [
  \text{min(8, 7)} \times (8 - 1) = 7 \times 7 = 49
  ]
* For bars at index `0` (height 1) and index `8` (height 7), the water capacity would be:
  [
  \text{min(1, 7)} \times (8 - 0) = 1 \times 8 = 8
  ]

You can see that the container formed by bars at indices 1 and 8 stores the most water (49 units).

### Key Insights:

* You can always reduce the problem to comparing different combinations of pairs of bars, but this would be inefficient (brute force), as it requires checking every pair, resulting in a time complexity of O(n²).
* A more efficient way to solve this is using the **two-pointer technique**.

### Two-pointer Approach:

1. **Start with two pointers**: One pointer at the beginning (`left = 0`) and one at the end (`right = len(heights) - 1`).
2. **Calculate the water stored** between the two bars.
3. **Move the pointers**:

   * If the bar at `left` is shorter, move the `left` pointer to the right (i.e., `left++`).
   * If the bar at `right` is shorter, move the `right` pointer to the left (i.e., `right--`).
4. Keep track of the maximum water you can store as you move the pointers.

This ensures that you only need to traverse the array once, leading to a time complexity of **O(n)**, which is much more efficient.

**C#**
```C#
public class Solution {
    public int MaxArea(int[] heights) {
        int i = 0;
        int j = heights.Length-1;
        int max = 0;
        while( i < j)
        {
            int minimum = heights[i] > heights[j] ? heights[j] : heights[i];
            int volume = (j-i) * minimum;
            if(volume > max)
            {
                max = volume;
            }
            if(heights[i] < heights[j])
            {
                i++;
            }
            else
            {
                j--;
            }
            
        }
        return max;
    }
}
```

**GPT's Insight**
Great question! The intuition behind **moving the pointers based on which height is smaller** is central to the efficiency of the two-pointer approach. Let’s break it down:

### Why Move the Shorter Pointer?

The key to solving this problem efficiently (in O(n) time) is recognizing that **the area between two bars** depends on two factors:

1. **The distance between the bars** (i.e., how far apart the indices are).
2. **The height of the shorter bar** (because water can't rise above the shorter bar).

If you imagine water trapped between two bars, no matter how wide the container (i.e., the distance between bars), the maximum volume is limited by the shorter of the two bars. This is because if the taller bar is on one side, the shorter bar on the other side limits the water level.

#### Now, why move the shorter bar?

* If the height of the bar on the left (`heights[i]`) is **smaller** than the height on the right (`heights[j]`), then the **left bar** is limiting the water volume because the height of the container is constrained by the shorter one. To **increase the height** (and possibly the area), you want to move the left pointer to the right, hoping to find a taller bar.

* Conversely, if the bar on the right (`heights[j]`) is **smaller** or equal, the **right bar** is limiting the water volume. So, you move the right pointer to the left to potentially find a taller bar.

### Intuition Behind the Pointer Movement:

Let’s say you have two bars, one taller and one shorter. The current area between them is determined by the distance between the bars and the shorter height. Here’s what you need to keep in mind:

* **If the shorter bar is on the left**, you move the left pointer (`i++`), hoping to find a taller bar on the left side that might give you a larger area.
* **If the shorter bar is on the right**, you move the right pointer (`j--`), hoping to find a taller bar on the right side.

The reasoning behind always moving the shorter bar is because **the taller bar** cannot limit the water capacity any more than it already does. It’s the shorter bar that’s the bottleneck. Moving the shorter bar might allow for a taller container with the other bar, which would increase the area.

### Why This Works Efficiently:

If you used a brute-force approach, you’d have to check every possible pair of bars to see which one forms the largest container. This would take O(n²) time, which is inefficient. However, by using the two-pointer approach:

* You **only pass through the array once** (O(n) time).
* You always try to find a larger container by moving the shorter bar, potentially increasing the height or keeping the width as large as possible.

By the time the pointers meet, you've evaluated all possible pairs of bars in a very efficient manner.

### Example Walkthrough:

Let’s walk through an example:

`heights = [1, 8, 6, 2, 5, 4, 8, 3, 7]`

1. Start with two pointers: `i = 0` and `j = 8`. The area is determined by:

   * **Height** = min(1, 7) = 1
   * **Width** = 8 - 0 = 8
   * **Area** = 1 * 8 = 8
     Now, move the pointer for the shorter bar, which is `heights[i] = 1`. So, we increment `i` to 1.

2. Now, `i = 1` and `j = 8`. The area is:

   * **Height** = min(8, 7) = 7
   * **Width** = 8 - 1 = 7
   * **Area** = 7 * 7 = 49
     This is a larger area, so update `max = 49`. Now, move the pointer for the shorter bar, which is `heights[j] = 7`. So, we decrement `j` to 7.

3. Now, `i = 1` and `j = 7`. The area is:

   * **Height** = min(8, 3) = 3
   * **Width** = 7 - 1 = 6
   * **Area** = 3 * 6 = 18
     The area is smaller, so we keep `max = 49`. Since `heights[i] = 8` is taller, we move `j` again (decrement `j`).

And so on... Until the pointers cross.

### Summary of the Intuition:

* You want to always move the pointer pointing to the **shorter bar** because it limits the water volume.
* By moving the shorter bar, you're attempting to increase the height and potentially increase the area.
* You only need to move one of the pointers at each step, which keeps the algorithm efficient (O(n)).


**Python**
```python
class Solution:
    def maxArea(self, heights: List[int]) -> int:
        maxResult = 0
        i = 0
        j = len(heights)-1
        while i < j:
            minimum = heights[j] if heights[i] > heights[j] else heights[i];
            volume = (j-i) * (minimum)
            maxResult = volume if volume > maxResult else maxResult
            if heights[i] > heights[j]:
                j-=1;
            else:
                i+=1;
        return maxResult
```

