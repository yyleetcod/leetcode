**Problem**

A sentence  `S`  is given, composed of words separated by spaces. Each word consists of lowercase and uppercase letters only.

We would like to convert the sentence to "_Goat Latin"_ (a made-up language similar to Pig Latin.)

The rules of Goat Latin are as follows:

-   If a word begins with a vowel (a, e, i, o, or u), append  `"ma"` to the end of the word.  
    For example, the word 'apple' becomes 'applema'.  
    
-   If a word begins with a consonant (i.e. not a vowel), remove the first letter and append it to the end, then add  `"ma"`.  
    For example, the word  `"goat"` becomes  `"oatgma"`.  
    
-   Add one letter  `'a'` to the end of each word per its word index in the sentence, starting with 1.  
    For example, the first word gets  `"a"`  added to the end, the second word gets  `"aa"`  added to the end and so on.

Return the final sentence representing the conversion from  `S` to Goat Latin.

> **Example 1:**
**Input:** "I speak Goat Latin"
**Output:** "Imaa peaksmaaa oatGmaaaa atinLmaaaaa"

>**Example 2:**
**Input:** "The quick brown fox jumped over the lazy dog"
**Output:** "heTmaa uickqmaaa rownbmaaaa oxfmaaaaa umpedjmaaaaaa overmaaaaaaa hetmaaaaaaaa azylmaaaaaaaaa ogdmaaaaaaaaaa"

**Solution**
```
class Solution {
public:
    string toGoatLatin(string S) {
        stringstream is(S);
        string word, a, ans;
        unordered_set<char> hash = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};
        while(is >> word){
            a.push_back('a');
            if(hash.count(word[0]))
                ans += word + "ma" + a + " ";
            else
                ans += word.substr(1) + word[0] + "ma" + a + " ";
        }
        ans.pop_back();
        return ans;
    }
};
```
Note: use i/o stringstream instead of stringsplit can make the code short.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExOTA5ODM5OTMsLTQ0OTQ1MTk3MywtOT
I4MDYxOTQ2XX0=
-->