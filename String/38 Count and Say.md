# **Problem**
The count-and-say sequence is the sequence of integers with the first five terms as following:

1.     1
2.     11
3.     21
4.     1211
5.     111221

`1`  is read off as  `"one 1"`  or  `11`.  
`11`  is read off as  `"two 1s"`  or  `21`.  
`21`  is read off as  `"one 2`, then  `one 1"`  or  `1211`.  

Given an integer  _n_, generate the  _n_th  term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

**Example 1:**

**Input:** 1
**Output:** "1"

**Example 2:**

**Input:** 4
**Output:** "1211"

# **Solution**

Use recursive solution, construct the answer for $countAndSay(n)$ from $countAndSay(n)$.
```
class Solution {
public:
    string countAndSay(int n) {
        if(n == 1)
            return "1";
        string s = countAndSay(n - 1), ans = "";
        int count = 1;
        for(int i = 1; i < s.size(); i++){
            if(s[i] == s[i - 1]){
                count++;
            }
            else{
                ans += to_string(count) + s[i - 1];
                count = 1;
            }
        }
        ans += to_string(count) + s[s.size() - 1];
        cout<<ans<<endl;
        return ans;
    }
};
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzQzMzQ1MDI0XX0=
-->