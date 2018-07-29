**Problem**
X is a good number if after rotating each digit individually by 180 degrees, we get a valid number that is different from X. Each digit must be rotated - we cannot choose to leave it alone.

A number is valid if each digit remains a digit after rotation. 0, 1, and 8 rotate to themselves; 2 and 5 rotate to each other; 6 and 9 rotate to each other, and the rest of the numbers do not rotate to any other number and become invalid.

Now given a positive number  `N`, how many numbers X from  `1`  to  `N`  are good?

**Example:**
**Input:** 10
**Output:** 4
**Explanation:** 
There are four good numbers in the range [1, 10] : 2, 5, 6, 9.
Note that 1 and 10 are not good numbers, since they remain unchanged after rotating.

**Solution**
- 1.For a number $a$ which is greater than 0 and less than $N + 1$, judge whether a is a good number.
```
class Solution {
public:
    int rotatedDigits(int N) {
        int ans = 0;
        for(int i = 1; i <= N; i++){
            if(isGood(i))
                ans++;
        }
        return ans;
    }
    bool isGood(int x){
        bool flag = false;
        while(x > 0){
            if(x % 10 == 3 || x % 10 == 4 || x % 10 == 7)
                return false;
            if(x % 10 == 2 || x % 10 == 5 || x % 10 == 6 || x % 10 == 9)
                flag = true;
            x = x / 10;
        }
        return flag;
    }
};
```
Time complexity: $O(nlogn)$
Space complexity: $O(1)$
- 2.DP: For a number $a$ which is greater than 0 and less than $N + 1$, define $b = a / 10, c = a \% 10$, $a$ is a good number if and only if ($b$ is a good number or $c$ is a good number.)
```
class Solution {
public:
    int rotatedDigits(int N) {
        vector<int> dp(N + 1, 0);
        int count = 0;
        for(int i = 0; i <= N; i++){
            if(i < 10){
                if(i == 1 || i == 0 || i == 8)
                    dp[i] = 1;
                else if(i == 2 || i == 5 || i == 6 || i == 9){
                    dp[i] = 2;
                    count++;
                }
            }
            else{
                int a = dp[i / 10], b = dp[i % 10];
                if(a == 1 && b == 1)
                    dp[i] = 1;
                else if(a >= 1 && b >= 1){
                    dp[i] = 2;
                    count++;
                }
            }
        }
        return count;
    }
};
```
Time complexity: $O(n)$
Space complexity: $O(n)$

- 3.Math:
Idea 1: If there are  $m$  digits remaining to be chosen, then there are  $(3+4)^m$possible valid numbers.
Since we are never choosing  invalid  numbers, we will always have  7  valid numbers to choose from per digit.
Idea #2: If a green number has been seen, each of the remaining  $(3+4)^m$  possible valid numbers are good numbers; otherwise,  $3^m$ of those valid numbers are not good numbers and must be subtracted from the over estimation.
If we have seen a  new number, then by definition, the number is considered good since it is a valid number. 
If we have not seen a  new number, one of the paths does not include any good numbers.
Idea #3: The less significant digits do not affect the good numbers contained in the more significant digits.
Consider the number  642. We can break this apart into the three distinct regions  [0,600),  [600,640),  [640,642). The less significant digits  4  and  2  will have no effect on the amount of good numbers in the  [0,600)  region.
```
class Solution {
public:
    int type[10] = {1, 1, 2, 0, 0, 2, 2, 0, 1, 2};
    int validrotation[10] = {1, 2, 3, 3, 3, 4, 5, 5, 6, 7};
    int differentrotation[10] = {0, 0, 1, 1, 1, 2, 3, 3, 3, 4};
    int samerotation[10] = {1, 2, 2, 2, 2, 2, 2, 2, 3, 3};
    int rotatedDigits(int N) {
        return FindGoodNumber(to_string(N), false);
    }
    
    int FindGoodNumber(string s, bool isnewnumber){
        int digit = s[0] - '0', ans = 0, len = s.size();
        if(len == 1)
            return isnewnumber? validrotation[digit] : differentrotation[digit];
        if(digit != 0){
            ans += validrotation[digit - 1] * pow(7, len - 1);
            if(!isnewnumber)
                ans -= samerotation[digit - 1] * pow(3, len - 1);
        }
        if(type[digit] == 2)
            isnewnumber = true;
        if(type[digit] != 0)
            ans += FindGoodNumber(s.substr(1, len - 1), isnewnumber);
        return ans;
    }
    
};
```
Time complexity: $O(logn)$
Space complexity: $O(1)$
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDY1MDgzMjgzXX0=
-->