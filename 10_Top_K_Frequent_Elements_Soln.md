https://neetcode.io/problems/top-k-elements-in-list?list=neetcode150

https://leetcode.com/problems/top-k-frequent-elements/description/

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

 

Example 1:

Input: nums = [1,1,1,2,2,3], k = 2

Output: [1,2]

Example 2:

Input: nums = [1], k = 1

Output: [1]

Example 3:

Input: nums = [1,2,1,2,1,2,3,1,3,2], k = 2

Output: [1,2]

 

Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104
k is in the range [1, the number of unique elements in the array].
It is guaranteed that the answer is unique.
 

Follow up: Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

**C# Better**
```C#
public class Solution {
    public int[] TopKFrequent(int[] nums, int k) {
        Dictionary<int,int> dict = new Dictionary<int,int>();
        for(int i=0; i<=nums.Length-1; i++)
        {
            if(dict.ContainsKey(nums[i]))
            {
                dict[nums[i]] += 1;
            }
            else
            {
                dict[nums[i]] = 1;
            }
        }
        return dict.OrderByDescending(x=>x.Value).Take(k).Select(x=>x.Key).ToArray();
    }
}
```
**Python Brute**
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        mapp = {}
        for element in nums:
            if element in mapp:
                mapp[element]+=1
            else:
                mapp[element]=1
        sortedList = sorted(mapp.items(),key=lambda x:x[1],reverse=True)
        result = []
        for item in sortedList[0:k]:
            result.append(item[0])
        return result
```

| Complexity Type      | Expression         | Worst Case     |
| -------------------- | ------------------ | -------------- |
| **Time Complexity**  | O(n + m log m + k) | **O(n log n)** |
| **Space Complexity** | O(m + k)           | **O(n)**       |


**GPT's Insight:**
Haha 😄 no worries bro — I got you!
Let’s break that “rocket science” down into **super easy steps** — you’ll totally get it. 🚀

---

Let’s start from here 👇

```python
mapp = {1: 3, 2: 2, 3: 1}
```

That means:

* number `1` appeared 3 times
* number `2` appeared 2 times
* number `3` appeared 1 time

Now you want the **top k** most frequent numbers — for example `k = 2`, you want `[1, 2]`.

---

### 💡 Step 1: What `mapp.items()` means

If you do:

```python
print(mapp.items())
```

You get:

```
dict_items([(1, 3), (2, 2), (3, 1)])
```

That’s just a **list of pairs**:

```
[(1, 3), (2, 2), (3, 1)]
```

Each pair means → `(number, count)`

---

### 💡 Step 2: Sorting those pairs

We want to sort them **by count** (the second number in each pair).

That’s what this line does:

```python
sorted_items = sorted(mapp.items(), key=lambda x: x[1], reverse=True)
```

Let’s read it in English:

* `sorted()` → sort a list
* `mapp.items()` → sort the pairs
* `key=lambda x: x[1]` → sort by the *second item* in each pair (the count)
* `reverse=True` → biggest first

So after sorting, we get:

```
[(1, 3), (2, 2), (3, 1)]
```

— already in order from most frequent to least.

---

### 💡 Step 3: Picking just the numbers

Now we don’t need the counts anymore — just the numbers (`1, 2, ...`).

That’s what this line does:

```python
result = [item[0] for item in sorted_items[:k]]
```

Read it like this:

* `sorted_items[:k]` → take the first k pairs (e.g. top 2)
* `item[0]` → get the first part of each pair (the number)
* `[ ... for ... in ... ]` → make a list out of those numbers

Example:

```
sorted_items[:2] = [(1, 3), (2, 2)]
result = [1, 2]
```

---

### ✅ Final version (simple and clean)

```python
class Solution:
    def topKFrequent(self, nums, k):
        mapp = {}
        for num in nums:
            if num in mapp:
                mapp[num] += 1
            else:
                mapp[num] = 1

        sorted_items = sorted(mapp.items(), key=lambda x: x[1], reverse=True)
        result = [item[0] for item in sorted_items[:k]]
        return result
```

---

### 💥 Example run:

```python
nums = [1,1,1,2,2,3]
k = 2
print(Solution().topKFrequent(nums, k))
```

**Output:**

```
[1, 2]
```

---

Would you like me to rewrite it in **even simpler “beginner style”** — like using normal loops instead of that `[item[0] for item in ...]` part?

Ahhh okay bro 😄 — now I get what’s confusing you.
You’re like: **“why do we even need that `key=` and that colon `:` after lambda?”**

Let’s make this crystal clear step-by-step 👇

---

## 🧩 1. What `sorted()` normally does

When you sort a simple list like this:

```python
nums = [5, 2, 8, 1]
sorted_nums = sorted(nums)
print(sorted_nums)
```

👉 Output:

```
[1, 2, 5, 8]
```

By default, it sorts based on the *value itself*.
That’s fine for numbers — it just compares `5`, `2`, `8`, `1`.

---

## 💡 2. But what if you have *pairs*?

Example:

```python
pairs = [(1, 3), (2, 2), (3, 1)]
```

If you just do:

```python
sorted(pairs)
```

👉 It sorts by the **first number** in each pair (the key):

```
[(1, 3), (2, 2), (3, 1)]
```

(because 1 < 2 < 3)

But we want to sort by the **second number** (the frequency), not the first.

---

## ⚙️ 3. That’s where `key=` comes in

When you write:

```python
sorted(pairs, key=lambda x: x[1])
```

You’re telling Python:

> “Hey, when comparing things, don’t look at the whole pair —
> look only at `x[1]` (the second value)!”

So `key=` is just a way to tell **what to sort by**.

It’s like saying:

* `key=` → “the rule for sorting”
* `lambda x: x[1]` → “the rule is: use the second value of each pair”

---

## 🧠 4. Why the colon (`:`) in `lambda`

That’s just how **lambda functions** are written in Python.
The structure is:

```
lambda <input>: <what to return>
```

So:

```python
lambda x: x[1]
```

means:

> "Take input `x`, and return `x[1]`."

It’s the same as writing:

```python
def temp_function(x):
    return x[1]
```

but shorter and inline.

---

## 🧩 5. So this line

```python
sorted_items = sorted(mapp.items(), key=lambda x: x[1], reverse=True)
```

can be read in plain English as:

> “Sort the pairs in `mapp.items()` by the second thing (`x[1]`), biggest first.”

---

### 🎯 Analogy time (to make it stick):

Imagine you have a list of students and their marks:

```python
students = [("Alex", 88), ("Ben", 92), ("Charlie", 75)]
```

Now you want to sort by **marks**, not by **name**.

👉 So you write:

```python
sorted(students, key=lambda x: x[1], reverse=True)
```

This means:

> “Sort students by their second thing (`x[1]`, the mark).”

---

### 🧠 TL;DR

| Piece    | Meaning                                          |
| -------- | ------------------------------------------------ |
| `key=`   | tells Python *what to look at* when sorting      |
| `lambda` | creates a tiny inline function                   |
| `:`      | separates input (`x`) and output (`x[1]`)        |
| `x[1]`   | the part of each pair we want to use for sorting |

---

**C# Better**
```C#
public class Solution {
    public int[] TopKFrequent(int[] nums, int k) {
        Dictionary<int,int> dict = new Dictionary<int,int>();
        for(int i=0; i<=nums.Length-1; i++)
        {
            if(dict.ContainsKey(nums[i]))
            {
                dict[nums[i]] += 1;
            }
            else
            {
                dict[nums[i]] = 1;
            }
        }
        PriorityQueue<int,int> minHeap = new PriorityQueue<int,int>();
        foreach(var item in dict)
        {
            minHeap.Enqueue(item.Key,item.Value);
            if(minHeap.Count>k)
            {
                minHeap.Dequeue();
            }
        }
        int[] result = new int[k];
        for(int i=0;i<k;i++)
        {
            result[i] = minHeap.Dequeue();
        }
        return result;
        //return dict.OrderByDescending(x=>x.Value).Take(k).Select(x=>x.Key).ToArray();
    }
}
```



Ahhh bro 😎 — now we’re getting into the **heap/priority queue magic**! Let me break it down super clearly.

---

## 1️⃣ What is a Priority Queue?

A **priority queue** is like a **special line at an amusement park**:

* Normal queue → first come, first served (FIFO)
* Priority queue → the person with the **highest priority** goes first, no matter when they arrived

In C#, `PriorityQueue<TElement, TPriority>` works like this:

```csharp
PriorityQueue<int, int> pq = new PriorityQueue<int, int>();
```

* `TElement` → the thing you want to store (`num`)
* `TPriority` → the “priority” of that thing (`count`)

Then:

* `Enqueue(element, priority)` → put element in the queue with a priority
* `Dequeue()` → removes the element with **highest priority** (or lowest, depends on min/max heap)

---

## 2️⃣ Why use a priority queue here?

Problem: “Return **top k most frequent numbers**”

* We **don’t care about all numbers**, only the **top k frequencies**
* Dictionary gives counts, but we need a **way to always keep track of top k efficiently**

Instead of **sorting the whole dictionary** (which is O(n log n)), we can use a **min-heap of size k**:

1. Push each number into the heap with its frequency as priority
2. If heap size > k → remove the **smallest frequency**
3. At the end → heap has **k numbers with largest frequency**

This makes the algorithm more efficient, especially when `n` is large.

---

## 3️⃣ Step-by-step explanation of your code

```csharp
var count = new Dictionary<int, int>();
foreach (var num in nums) {
    if (count.ContainsKey(num)) {
        count[num]++;
    } else {
        count[num] = 1;
    }
}
```

✅ Count frequency of each number (same as before).

---

```csharp
var heap = new PriorityQueue<int, int>();
foreach (var entry in count) {
    heap.Enqueue(entry.Key, entry.Value);
    if (heap.Count > k) {
        heap.Dequeue();
    }
}
```

* Loop over each `(num, freq)` pair
* Push `num` into the heap with priority = `freq`
* Keep heap **size ≤ k** → always pop the **smallest frequency**
* At the end → heap contains **top k frequent numbers only**

---

```csharp
var res = new int[k];
for (int i = 0; i < k; i++) {
    res[i] = heap.Dequeue();
}
```

* Pop all elements from the heap into the result array

⚠️ Note: The numbers may **not be sorted by frequency** in `res` — if you want sorted, you can sort `res` afterwards.

---

## 4️⃣ Why priority queue vs sorting?

| Method                              | Time Complexity                 |
| ----------------------------------- | ------------------------------- |
| Sort dictionary by frequency        | O(n log n)                      |
| Min-heap / priority queue of size k | O(n log k) ✅ faster when k << n |

So using a **priority queue** is a **more efficient way** to get top k frequent numbers.

---

### 🧠 Analogy

Imagine you have 1 million students and you want the **top 3 scorers**:

* Sorting everyone → huge work (1 million × log 1 million)
* Heap → just maintain **top 3** while reading the scores → much faster

---
Ahhh bro 😎 — now we’re getting to the **core of heaps**. Let’s break it down nice and slow.

---

## 1️⃣ What is a heap?

A **heap** is a **special binary tree** with one main property:

* Every parent node is **smaller or bigger** than its children, depending on the type of heap.

There are **two types**:

---

### 🔹 Min-Heap

* Parent node ≤ children nodes
* The **smallest element is always at the top** (root)
* Think of it like a priority queue where **lowest priority comes out first**

Example:

```
       1
     /   \
    3     5
   / \
  4   6
```

* Top (root) = 1 → smallest element
* Every parent ≤ children

---

### 🔹 Max-Heap

* Parent node ≥ children nodes
* The **largest element is always at the top** (root)

Example:

```
       6
     /   \
    4     5
   / \
  1   3
```

* Top (root) = 6 → largest element
* Every parent ≥ children

---

## 2️⃣ What makes it a **min-heap or max-heap**?

* It’s determined by **how you compare priorities** when inserting.
* In C# `PriorityQueue<TElement, TPriority>`:

```csharp
var heap = new PriorityQueue<int, int>();
```

* By default → **min-heap** on the `TPriority`
* That means **smallest priority comes out first** when you `Dequeue()`

---

## 3️⃣ What about `if (heap.Count > k)`?

That line is **not what makes it a min-heap**, bro 😄

```csharp
if (heap.Count > k)
    heap.Dequeue();
```

* This line is just **keeping the heap size ≤ k**
* Because we only care about the **top k frequent numbers**
* Since it’s a **min-heap**, `Dequeue()` removes the **smallest frequency**
* That way, the heap always contains the **k largest frequencies**

---

### 4️⃣ How it works in your code:

Say counts are:

```
num → freq
1 → 5
2 → 2
3 → 3
```

Step by step with k=2:

1. Push 1 → heap = [1(5)]
2. Push 2 → heap = [2(2), 1(5)] (min-heap on frequency → 2 at top)
3. Push 3 → heap = [3(3), 1(5), 2(2)] → count > k, so `Dequeue()` → removes 2(2)

✅ Heap now contains: [3(3), 1(5)] → **top 2 frequent numbers**

---

### 🔹 Key Points

| Concept            | Explanation                                                   |
| ------------------ | ------------------------------------------------------------- |
| Min-Heap           | Smallest priority at top                                      |
| Max-Heap           | Largest priority at top                                       |
| Makes it min-heap? | Comparison function on priorities (default in C# is min-heap) |
| `heap.Count > k`   | Not what makes it min-heap — just keeps heap size ≤ k         |

---

If you want, bro, I can **draw the heap as a tree with numbers and frequencies** for your example — it makes the whole min-heap idea visually clear.

Do you want me to do that?
Ahhh bro 😎 — here’s the straight-up syntax for **min-heap and max-heap in C#** using `PriorityQueue<TElement, TPriority>`:

---

## 1️⃣ Min-Heap (default)

In C#, `PriorityQueue` is **min-heap by default**, meaning **smallest priority comes out first**.

```csharp
// Min-Heap: smallest priority dequeued first
var minHeap = new PriorityQueue<int, int>();

// Enqueue: element, priority
minHeap.Enqueue(10, 10); // element=10, priority=10
minHeap.Enqueue(20, 5);  // element=20, priority=5
minHeap.Enqueue(30, 15); // element=30, priority=15

// Dequeue removes the element with **smallest priority**
Console.WriteLine(minHeap.Dequeue()); // Output: 20
```

---

## 2️⃣ Max-Heap

C#’s built-in `PriorityQueue` does **not have a built-in max-heap**, but we can **invert the priority**:

```csharp
// Max-Heap: largest priority dequeued first
var maxHeap = new PriorityQueue<int, int>();

// To make it max-heap, store -priority
maxHeap.Enqueue(10, -10); 
maxHeap.Enqueue(20, -5);  
maxHeap.Enqueue(30, -15); 

// Dequeue removes element with **largest original priority**
Console.WriteLine(maxHeap.Dequeue()); // Output: 10
```

✅ Trick: Negate the priority to turn min-heap into max-heap.

---

### 3️⃣ Quick summary

| Heap type | Default C# behavior            | How to make it                               |
| --------- | ------------------------------ | -------------------------------------------- |
| Min-Heap  | Yes (smallest priority on top) | Just use `PriorityQueue` normally            |
| Max-Heap  | No                             | Negate priority when enqueuing (`-priority`) |

---

If you want, bro, I can make a **tiny visual diagram showing min vs max heap with numbers and priorities** — it helps this “magic” stick instantly.

Do you want me to do that?


**Note: Read its python version**


**Python optimised**
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        mapp = {}
        for element in nums:
            if element in mapp:
                mapp[element]+=1
            else:
                mapp[element]=1
        # sortedList = sorted(mapp.items(),key=lambda x:x[1],reverse=True)
        # result = []
        # for item in sortedList[0:k]:
        #     result.append(item[0])
        # return result
        bucket = [[] for _ in range(len(nums)+1)]
        for key,value in mapp.items():
            bucket[value].append(key)
        
        result = []
        for i in range(len(bucket)-1,0,-1):
            for j in bucket[i]:
                result.append(j)
                if len(result)==k:
                    return result
```


**Prerequisite:**
Bucket sort
Min Heap
