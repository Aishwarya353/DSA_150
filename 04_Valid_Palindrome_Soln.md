https://leetcode.com/problems/valid-palindrome/description/

https://neetcode.io/problems/is-palindrome?list=neetcode150

**Description**

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

 

Example 1:

Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
Example 2:

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
Example 3:

Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
 

Constraints:

1 <= s.length <= 2 * 105
s consists only of printable ASCII characters.

----

Pattern : Two Pointer Approach

-----

**C#**

    public class Solution {
        public bool IsPalindrome(string s) {
            int left =0;
            int right = s.Length-1;
            while(left < right)
            {
                while(left < right && !char.IsLetterOrDigit(s[left])) left++;
                while(left < right && !char.IsLetterOrDigit(s[right])) right--;
                if(char.ToLower(s[left])!=char.ToLower(s[right]))
                {
                    return false;
                }
                left++;
                right--;
            }
            return true;
        }
    }

**Python**

    class Solution:
        def isPalindrome(self, s: str) -> bool:
            left = 0
            right = len(s)-1
            while(left < right):
                while(left < right and not s[left].isalnum()):
                    left+=1
                while(left < right and not s[right].isalnum()):
                    right-=1
                if s[left].lower() != s[right].lower():
                    return False
                left+=1
                right-=1
            return True         

