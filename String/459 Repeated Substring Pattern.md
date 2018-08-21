# **Problem**
Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.

**Example 1:**

**Input:** "abab"
**Output:** True
**Explanation:** It's the substring "ab" twice.

**Example 2:**

**Input:** "aba"
**Output:** False

**Example 3:**

**Input:** "abcabcabcabc"
**Output:** True
**Explanation:** It's the substring "abc" four times. (And the substring "abcabc" twice.)

# **Solution**
1. For every $i$ which $len\%i==0$, reverse the initial string $s$ to a new string $t$, where $t=s(i,end)+s(0,i-1)$. Return true if and only if $t == s$.
```
class Solution {
public:
    bool repeatedSubstringPattern(string s) {
        int len = s.size();
        if(len == 0)
            return false;
        for(int i = 1; i <= len / 2; i++){
            if(len % i == 0){
                string t = reversestring(s, i);
                if(t == s)
                    return true;
            }
        }
        return false;
    }
    string reversestring(string s, int i){
        string t = s.substr(i);
        t += s.substr(0, i);
        return t;
    }
};
```
2. For every $i$ which $len\%i==0$, generate a new string $t$, where $t=m * s(0,i-1)$, $m=len/i$. Return true if and only if $t == s$.
```
class Solution {
public:
    bool repeatedSubstringPattern(string s) {
        int len = s.size();
        if(len == 0)
            return false;
        for(int i = 1; i <= len / 2; i++){
            if(len % i == 0){
                int m = len / i;
                string t = "";
                for(int j = 0; j < m; j++)
                    t += s.substr(0, i);
                if(t == s)
                    return true;
            }
        }
        return false;
    }
};
```
3. Generate a new string $t=(s+s)$, and remove the first and last character of $t$. Return true if and only if $s$ is a substring of $t$.
```
class Solution {
public:
    bool repeatedSubstringPattern(string s) {
        if(s.size() <= 1)
            return false;
        string ss = s + s;
        ss = ss.substr(1, ss.size() - 2);
        for(int i = 0; i <= ss.size() - s.size(); i++){
            string t = ss.substr(i, s.size());
            if(t == s)
                return true;
        }
        return false;
    }
};
```
4. We can improve the *solution 3* by using KMP to check whether $s$ is a substring of $t$.
```
class Solution {
public:
    bool repeatedSubstringPattern(string s) {
        if(s.size() <= 1)
            return false;
        string ss = s + s;
        ss = ss.substr(1, ss.size() - 2);
        return(KMP(ss, s));
    }
    bool KMP(string ss, string s){
        vector<int> nextidx = getnext(s);
        int len_ss = ss.size(), len_s = s.size(), i = 0, j = 0;
        while(i < len_ss && j < len_s){
            if(j == -1 || ss[i] == s[j]){
                i++;
                j++;
            }
            else
                j = nextidx[j];
        }
        if(j == len_s)
            return true;
        return false;
    }
    vector<int> getnext(string s){
        vector<int> ans(s.size() + 1);
        int j = -1;
        ans[0] = -1;
        for(int i = 0; i < s.size(); i++){
            if(j == -1 || s[i] == s[j]){
                i++;
                j++;
                if(s[i] != s[j])
                    ans[i] = j;
                else
                    ans[i] = ans[j];
            }
            else
                j = ans[j];
        }
        return ans;
    }
};
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjg4NDU0ODQxLDkwNjI1ODQwM119
-->