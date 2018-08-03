# Problem
Given a non-empty string  `s`, you may delete  **at most**  one character. Judge whether you can make it a palindrome.

**Example 1:**  

**Input:** "aba"
**Output:** True

**Example 2:**  

**Input:** "abca"
**Output:** True
**Explanation:** You could delete the character 'c'.

# Solution
**Intuition**

If the beginning and end characters of a string are the same (ie.  `s[0] == s[s.length - 1]`), then whether the inner characters are a palindrome (`s[1], s[2], ..., s[s.length - 2]`) uniquely determines whether the entire string is a palindrome.

**Algorithm**

Suppose we want to know whether  `s[i], s[i+1], ..., s[j]`  form a palindrome. If  `i >= j`  then we are done. If  `s[i] == s[j]`  then we may take  `i++; j--`. Otherwise, the palindrome must be either  `s[i+1], s[i+2], ..., s[j]`  or  `s[i], s[i+1], ..., s[j-1]`, and we should check both cases.

```
class Solution {
public:
    bool validPalindrome(string s) {
        int len = s.size();
        for(int i = 0; i < len / 2; i++){
            if(s[i] != s[len - 1 - i]){
                int j = len - 1 - i;
                return isPalindrome(s, i + 1, j) || isPalindrome(s, i, j - 1);
            }
        }
        return true;
    }
    bool isPalindrome(string s, int i, int j){
        for(int k = i; k <= i + (j - i) / 2; k++){
            if(s[k] != s[i + j - k])
                return false;
        }
        return true;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU4MDIwNTg1Ml19
-->