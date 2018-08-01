# **Problem**
Count the number of segments in a string, where a segment is defined to be a contiguous sequence of non-space characters.

Please note that the string does not contain any  **non-printable**  characters.

**Example:**

**Input:** "Hello, my name is John"
**Output:** 5

# **Solution**
```
class Solution {
public:
    int countSegments(string s) {
        int count = 0;
        for(int i = 0; i < s.size(); i++){
            if(s[i] != ' ' && (i == 0 || s[i - 1] == ' '))
                count++;
        }
        return count;
    }
};
```
Or use **isstringstream**
```
class Solution {
public:
    int countSegments(string s) {
        istringstream in(s);
        int count = 0;
        while(in >> s)
            count++;
        return count;
    }
};
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NjY5NDc1MTVdfQ==
-->