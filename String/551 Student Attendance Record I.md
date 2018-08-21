**Problem**
You are given a string representing an attendance record for a student. The record only contains the following three characters:

1.  **'A'**  : Absent.
2.  **'L'**  : Late.
3.  **'P'**  : Present.

A student could be rewarded if his attendance record doesn't contain  **more than one 'A' (absent)**  or  **more than two continuous 'L' (late)**.

You need to return whether the student could be rewarded according to his attendance record.

**Example 1:**  

**Input:** "PPALLP"
**Output:** True

**Example 2:**  

**Input:** "PPALLL"
**Output:** False

**Solution**
- 1. Check whether number of char '$A$' is more than 1;
- 2. Check whether there is more than 2 continuous '$L$';
```
class Solution {
public:
    bool checkRecord(string s) {
        int cntA = 0, cntL = 0;
        for(auto c : s){
            if(c == 'A')
             cntA++;
            if(c == 'L')
                cntL++;
            else
                cntL = 0;
            if(cntA > 1 || cntL > 2)
                return false;
        }
        return true;
    }
};
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk1NzU3NjA4OSwtMTczOTI4Nzk3Ml19
-->