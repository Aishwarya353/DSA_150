**Daily Challenge 18 november 2025**

https://leetcode.com/problems/1-bit-and-2-bit-characters/description/?envType=daily-question&envId=2025-11-18

We have two special characters:

The first character can be represented by one bit 0.
The second character can be represented by two bits (10 or 11).
Given a binary array bits that ends with 0, return true if the last character must be a one-bit character.

 

Example 1:

Input: bits = [1,0,0]
Output: true
Explanation: The only way to decode it is two-bit character and one-bit character.
So the last character is one-bit character.
Example 2:

Input: bits = [1,1,1,0]
Output: false
Explanation: The only way to decode it is two-bit character and two-bit character.
So the last character is not one-bit character.
 

Constraints:

1 <= bits.length <= 1000
bits[i] is either 0 or 1.

**Python**
```Python
class Solution:
    def isOneBitCharacter(self, bits: List[int]) -> bool:
        i=0
        while i < len(bits)-1:
            if bits[i] == 0:
                i+=1
            else:
                i+=2
        return i == len(bits)-1
```


**GPT's Insight**
No worries bro — let me explain it **super simple**, like you're 5 years old.
After this, you’ll *never* get confused again. 😎

---

# 🧠 **The Entire Idea in One Sentence**

The array is a string of bits (0s and 1s).
Some characters take **1 bit** (just `0`),
some characters take **2 bits** (they always **start with 1**, like `10` or `11`).

That's it.

---

# 🎨 **Let’s Visualize It**

Think of the input like a tape:

```
bits = [1, 0, 1, 1, 0]
```

You must read characters from left to right.

There are two possible character types:

---

## ⭐ **1-bit character**

This character is **only one bit long**:

```
0
```

When you see `0`, it represents a single character.

So:

```
0
```

is one character.

---

## ⭐⭐ **2-bit character**

This character is **two bits long**, and it always **starts with 1**:

```
10   or   11
```

So anytime you see a `1`, it **must be the start of a 2-bit character**.

Examples:

```
10  is one character  
11  is one character
```

---

# 🧩 **Let’s decode an example**

### Example:

```
bits = [1,0,0]
```

Walk through:

1. See `1` → must be start of 2-bit char → use `10`
   (covers index 0 and 1)
2. Next we land on index 2 → it's `0` → 1-bit char

End with a `0` → last char is 1-bit → TRUE.

---

### Another example:

```
bits = [1,1,0]
```

Walk:

1. See `1` → 2-bit char → use `11`
2. Next we land on index 2 → it's `0` → 1-bit char

Again ends with `0` → TRUE.

---

### Example where last char is NOT 1-bit:

```
bits = [1,1,1,0]
```

Walk:

1. i=0 → bits[0]=1 → consume `11` → i=2
2. i=2 → bits[2]=1 → consume `10` → i=4 (past end!)

We skipped the last zero.
It wasn’t a standalone 1-bit character — it was part of a 2-bit character.

So answer is **FALSE**.

---

# 🧠 **Rule Summary**

| Bit pattern | Length | Meaning         |
| ----------- | ------ | --------------- |
| `0`         | 1 bit  | 1-bit character |
| `10`        | 2 bits | 2-bit character |
| `11`        | 2 bits | 2-bit character |

---

# 🎯 Final Goal of the Problem

**Check whether the *last* `0` in the array is a separate 1-bit character.**

If yes → return True
If it was part of a 2-bit character → return False

---

No problem bro, this line confuses **everyone** at first.

Let me explain it in the simplest way possible — **with pictures**.

---

# 🧠 **THE FINAL LINE**

```python
return i == len(bits) - 1
```

This line means:

👉 **Did we stop EXACTLY on the last index?**

If YES → last bit is a 1-bit character → return True
If NO → we jumped past it → last bit was part of a 2-bit → return False

---

# 🎨 VISUAL EXPLANATION

Imagine the bits:

```
index: 0 1 2 3
bits:  1 1 0 0
```

`len(bits) = 4`
So last index = `len(bits) - 1 = 3`

So this line:

```
return i == 3
```

It asks: **Did my pointer land exactly on 3?**

---

# 🍔 Why does landing exactly on last index mean TRUE?

Because:

### ✔ If you land ON the last bit,

that means you **read everything before it**,
and the last `0` was read alone → a 1-bit character.

### ❌ If you jump PAST the last bit,

that means the last `0` got **absorbed** as part of a 2-bit character → not 1-bit.

---

# 📌 Let's do examples so your brain locks it

---

# ✅ Example 1

```
bits = [1, 0, 0]
index:  0  1  2
```

Walk:

* i=0 → see 1 → jump +2 → i = 2 (LAST index)

So:

```
i == 2?
len(bits)-1 = 2
```

✔ True → last is a 1-bit

---

# ❌ Example 2

```
bits = [1, 1, 1, 0]
index:  0  1  2  3
```

Walk:

* i=0 → see 1 → jump to 2
* i=2 → see 1 → jump to 4 (past last)

Now:

```
i == 3 ?  # last index = 3
```

i = 4 → ❌ NOT equal

❌ False → last bit was part of a 2-bit character.

---

# 🧠 TL;DR in caveman English

```
If pointer stops ON last bit → True
If pointer jumps PAST last bit → False
```

The code checks exactly that.

---

# Want me to rewrite that line to make it clearer?

For example:

```python
is_last_one_bit = (i == len(bits) - 1)
return is_last_one_bit
```

Got you bro — let me explain **ONLY using the value of `i`**, nothing else.
By the end of this, you’ll 100% get it.

---

# 🧠 VERY IMPORTANT RULE

👉 **After finishing the loop, `i` tells us where we ended.**

We only care about ONE thing:

### ✔ If `i` equals the last index → last bit is a 1-bit

### ❌ If `i` goes past the last index → last bit is NOT 1-bit

That’s what this checks:

```python
return i == len(bits) - 1
```

---

# 🔥 NOW LET’S EXPLAIN WITH REAL `i` VALUES

## 👉 Case 1: `i` stops **AT** last index → TRUE

### Example:

```
bits = [1,0,0]
indexes: 0 1 2
```

Walk:

* i = 0 → bits[0] = 1 → jump +2 → i = 2
* Now i = 2 (last index)

Final check:

```
i == len(bits)-1 → 2 == 2 → True
```

### Meaning:

You landed ON the last zero → it is a **1-bit** character.

---

## 👉 Case 2: `i` goes **PAST** last index → FALSE

### Example:

```
bits = [1,1,1,0]
indexes: 0 1 2 3
```

Walk:

* i = 0 → bits[0]=1 → jump to i=2
* i = 2 → bits[2]=1 → jump to i=4  ❌ past last index

Last index = 3
But i = 4

Final check:

```
i == len(bits)-1 → 4 == 3 → False
```

### Meaning:

You *skipped over* the last zero → it was part of a **2-bit** character.

---

## 👉 Case 3: `i` lands somewhere before last index (should not happen), but if it did → FALSE

### Example:

```
bits = [0,0]
indexes: 0 1
```

Walk:

* i = 0 → bits[0]=0 → i=1
* Loop stops because i == last index

Now i = 1

Check:

```
1 == 1 → True
```

Correct → last is 1-bit.

---

# 🧠 SO THE VALUE OF `i` DECIDES EVERYTHING

### ✔ If final `i` = last index

```
i == len(bits)-1 → True
```

Means:

* pointer stopped **on** last 0
* last bit is a **1-bit character**

---

### ❌ If final `i` > last index

```
i == len(bits)-1 → False
```

Means:

* pointer **jumped over** the last 0
* last bit was part of a **2-bit character**

---

# 🏁 FINAL SUMMARY USING ONLY `i`

| Final `i` value   | Meaning                            | Return |
| ----------------- | ---------------------------------- | ------ |
| `i == last index` | last bit is a **1-bit**            | True   |
| `i > last index`  | last bit got **absorbed** in 2-bit | False  |

---

Ah, bro, now I get exactly what’s confusing you — the **while loop condition**:

```python
while i < len(bits) - 1:
```

Let me break it down super clearly using **`i` values**.

---

# 🧠 **What `len(bits) - 1` Means**

* `len(bits)` = total number of bits in the array
* Last index = `len(bits) - 1`
  (because Python arrays are 0-indexed)

So `len(bits) - 1` points to the **last bit** in the array.

---

# 🔹 **Why `< len(bits) - 1` and not `< len(bits)`?**

Remember:

* The **last bit is always 0**
* We want to see if it’s a 1-bit character **at the end**
* We **don’t need to process it inside the loop**; we only want to process **all bits before the last one**

So the loop stops **before the last index**:

```text
i < len(bits) - 1
```

---

# 🔹 **Step-by-step with i values**

### Example:

```
bits = [1, 0, 0]
indexes: 0 1 2
```

* `len(bits) = 3` → last index = 2
* Loop condition: `i < 2` → i can be 0 or 1

---

### Walk the loop:

1. i = 0 → bits[0]=1 → 2-bit char → i += 2 → i = 2

   * Now i == 2 → NOT less than 2 → loop stops
   * We **stopped exactly at last index** → check outside loop

2. i == last index → True → last bit is 1-bit char ✅

---

### Another example:

```
bits = [1, 1, 1, 0]
indexes: 0 1 2 3
```

* `len(bits) = 4` → last index = 3
* Loop condition: i < 3 → i can be 0,1,2

Walk:

1. i = 0 → bits[0]=1 → i +=2 → i=2
2. i = 2 → bits[2]=1 → i +=2 → i=4

Now i = 4 → NOT < 3 → loop stops

* i = 4 → jumped past last index → last bit NOT 1-bit ❌

---

# ✅ **TL;DR**

`while i < len(bits) - 1` means:

* Keep processing characters **until the bit right before the last one**
* We stop **before the last 0** because the last 0 is what we are checking **at the end**
* Then we just check **if i landed exactly on last index** → last bit is 1-bit

---

----
----
----
----

**Daily Challenge 19 november 2025**
https://leetcode.com/problems/keep-multiplying-found-values-by-two/description/?envType=daily-question&envId=2025-11-19

You are given an array of integers nums. You are also given an integer original which is the first number that needs to be searched for in nums.

You then do the following steps:

If original is found in nums, multiply it by two (i.e., set original = 2 * original).
Otherwise, stop the process.
Repeat this process with the new number as long as you keep finding the number.
Return the final value of original.

 

Example 1:

Input: nums = [5,3,6,1,12], original = 3
Output: 24
Explanation: 
- 3 is found in nums. 3 is multiplied by 2 to obtain 6.
- 6 is found in nums. 6 is multiplied by 2 to obtain 12.
- 12 is found in nums. 12 is multiplied by 2 to obtain 24.
- 24 is not found in nums. Thus, 24 is returned.
Example 2:

Input: nums = [2,7,9], original = 4
Output: 4
Explanation:
- 4 is not found in nums. Thus, 4 is returned.
 

Constraints:

1 <= nums.length <= 1000
1 <= nums[i], original <= 1000

**C#**
```C#
public class Solution {
    public int FindFinalValue(int[] nums, int original) {
        HashSet<int> sett = new HashSet<int>(nums);
        while(sett.Contains(original))
        {
            original*=2;
        }
        return original;
    }
}
```

**Python**
```python
class Solution:
    def findFinalValue(self, nums: list[int], original: int) -> int:
        # Keep doubling original while it exists in the nums array
        while original in nums:
            original *= 2

        return original
```
