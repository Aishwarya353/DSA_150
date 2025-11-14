https://leetcode.com/problems/valid-sudoku/

https://neetcode.io/problems/valid-sudoku?list=neetcode150

Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

Each row must contain the digits 1-9 without repetition.
Each column must contain the digits 1-9 without repetition.
Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.
Note:

A Sudoku board (partially filled) could be valid but is not necessarily solvable.
Only the filled cells need to be validated according to the mentioned rules.
 

Example 1:


Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
Example 2:

Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
 

Constraints:

board.length == 9
board[i].length == 9
board[i][j] is a digit 1-9 or '.'.


**C# Brute**
```C#
public class Solution {
    public bool IsValidSudoku(char[][] board) {
        //Rows
        for(int i=0; i<=8; i++)
        {
            HashSet<char> mapp = new HashSet<char>();
            for(int j=0; j<=8; j++)
            {
                if(board[i][j] == '.')
                    continue;
                if(mapp.Contains(board[i][j]))
                {
                    return false;
                }
                else
                {
                    mapp.Add(board[i][j]);
                }
            }
        }
        //Columns
        for(int i=0; i<=8; i++)
        {
            HashSet<char> mapp = new HashSet<char>();
            for(int j=0; j<=8; j++)
            {
                if(board[j][i] == '.')
                    continue;
                if(mapp.Contains(board[j][i]))
                {
                    return false;
                }
                else
                {
                    mapp.Add(board[j][i]);
                }
            }
        }
        //3 * 3 Boxes
        for(int i=0; i<=3-1; i++)
        {
            for(int j=0; j<=3-1; j++)
            {
                HashSet<char> mapp = new HashSet<char>();
                for(int r = i * 3; r <= i*3 + 3 - 1; r++)
                {
                    for(int c = j * 3; c <= j*3 + 3 - 1; c++)
                    {
                        if(board[r][c]=='.')
                            continue;
                        if(mapp.Contains(board[r][c]))
                        {
                            return false;
                        }
                        else
                        {
                            mapp.Add(board[r][c]);
                        }
                    }
                }
            }
        }
        return true;
    }
}
```

**Python Brute**
```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        #Rows
        for i in range(9):
            sett = set()
            for j in range(9):
                if board[i][j] == '.':
                    continue
                if board[i][j] in sett:
                    return False
                else:
                    sett.add(board[i][j])
        #Columns
        for i in range(9):
            sett = set()
            for j in range(9):
                if board[j][i] == '.':
                    continue
                if board[j][i] in sett:
                    return False
                else:
                    sett.add(board[j][i])
        # 3 * 3 Boxes
        for i in range(3):
            for j in range(3):
                sett = set()
                for r in range(i*3,i*3+3):
                    for c in range(j*3,j*3+3):
                        if board[r][c] == '.':
                            continue
                        if board[r][c] in sett:
                            return False
                        else:
                            sett.add(board[r][c])
        return True;
```

**GPT's Insight**
Say less bro — here is a **clean, simple, future-proof summary** you can save, screenshot, or write in your notes.

# 🔥 VALID SUDOKU — ULTIMATE SUMMARY (EASY TO REMEMBER)

A Sudoku board is **valid** if ALL of these are true:

---

# ✅ **1. ROW CHECK**

Loop each row and ensure no duplicates.

### Pattern:

```
for each row i:
    create empty set
    for each column j:
        if board[i][j] is digit:
            if digit in set → invalid
            else add digit
```

### Key idea:

* Fix the **row**, move across **columns**
* Access uses: `board[row][col]`

---

# ✅ **2. COLUMN CHECK**

Same logic as rows but flip the loops.

### Pattern:

```
for each column j:
    create empty set
    for each row i:
        if board[i][j] is digit:
            if digit in set → invalid
            else add digit
```

### Key idea:

* Fix the **column**, move down **rows**
* Access still: `board[row][col]`
* Just swap loops

---

# ✅ **3. 3×3 BOX CHECK**

There are **9 boxes**, each of size 3×3.

Boxes start at (row, col):

```
(0,0), (0,3), (0,6)
(3,0), (3,3), (3,6)
(6,0), (6,3), (6,6)
```

### Pattern:

```
for boxRow in 0..2
    for boxCol in 0..2
        create empty set
        for r in boxRow*3 .. boxRow*3+2
            for c in boxCol*3 .. boxCol*3+2
                if board[r][c] is digit:
                    if digit in set → invalid
                    else add digit
```

### Key idea:

* Each box is identified by (boxRow, boxCol)
* Multiply by **3** to get actual board index
* Always iterate EXACTLY 3 rows × 3 columns

---

# 🧠 **HOW TO REMEMBER FOREVER (BRO TIPS)**

### 🎯 **Row = horizontal**

Fix row → move left to right.

### 🎯 **Column = vertical**

Fix col → move top to bottom.

### 🎯 **Box = chunk of 3×3**

Row chunk = `0–2`, `3–5`, `6–8`
Col chunk = `0–2`, `3–5`, `6–8`

### 🎯 Boxes use 3-multiples:

```
0 * 3 = 0
1 * 3 = 3
2 * 3 = 6
```

So the start positions of every 3×3 box are always:

```
(0,0) (0,3) (0,6)
(3,0) (3,3) (3,6)
(6,0) (6,3) (6,6)
```

---

# ⭐ FINAL MENTAL MODEL

| Check  | What changes?        | What stays same?                        |
| ------ | -------------------- | --------------------------------------- |
| Row    | i fixed, j moves     | access board[i][j]                      |
| Column | j fixed, i moves     | access board[i][j]                      |
| Box    | boxRow, boxCol loops | inner loops use r, c, still board[r][c] |

Everything is just looping in different directions while always checking duplicates using a **HashSet**.

---

# Want a mini cheat-sheet version too?

```
ROW:    for i in 0..8 → for j in 0..8 → board[i][j]

COLUMN: for j in 0..8 → for i in 0..8 → board[i][j]

BOXES:  for br in 0..2 → for bc in 0..2 →
            for r in br*3..br*3+2 →
                for c in bc*3..bc*3+2 → board[r][c]
```

---
---
---
---


**C#**
```C#
public class Solution {
    public bool IsValidSudoku(char[][] board) {
        List<HashSet<char>> rows = new List<HashSet<char>>();
        List<HashSet<char>> columns = new List<HashSet<char>>();
        List<HashSet<char>> boxes = new List<HashSet<char>>();
        for(int k=0; k<=9-1; k++)
        {
            rows.Add(new HashSet<char>());
            columns.Add(new HashSet<char>());
            boxes.Add(new HashSet<char>());

        }
        for(int i=0; i<=8; i++)
        {
            for(int j=0; j<=8; j++)
            {
                if(board[i][j] == '.')
                    continue;
                if(rows[i].Contains(board[i][j]))
                return false;
                rows[i].Add(board[i][j]);

                if(columns[j].Contains(board[i][j]))
                return false;
                columns[j].Add(board[i][j]);

                int index = (i / 3) * 3 + (j/3);
                if(boxes[index].Contains(board[i][j]))
                return false;
                boxes[index].Add(board[i][j]);

            }
        }
        return true;
    }
}
```

**Python**
```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        rows = [set() for _ in range(9)]
        columns = [set() for _ in range(9)]
        boxes = [set() for _ in range(9)]

        for i in range(9):
            for j in range(9):
                if board[i][j] == '.':
                    continue
                if board[i][j] in rows[i]:
                    return False
                rows[i].add(board[i][j])

                if board[i][j] in columns[j]:
                    return False
                columns[j].add(board[i][j])

                index = (i//3) * 3 + (j//3)

                if board[i][j] in boxes[index]:
                    return False
                boxes[index].add(board[i][j])
        return True;
```
