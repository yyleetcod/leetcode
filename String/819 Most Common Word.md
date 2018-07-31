# **Problem**
Given a paragraph and a list of banned words, return the most frequent word that is not in the list of banned words. It is guaranteed there is at least one word that isn't banned, and that the answer is unique.

Words in the list of banned words are given in lowercase, and free of punctuation. Words in the paragraph are not case sensitive. The answer is in lowercase.

**Example:**
**Input:** 
paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
banned = ["hit"]
**Output:** "ball"
**Explanation:** 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.

# Solution
```
class Solution {
public:
    string mostCommonWord(string paragraph, vector<string>& banned) {
        paragraph += '.';
        string ans = "", word = "";
        int ansfreq = 0;
        unordered_set<string> bannedword;
        for(string s : banned)
            bannedword.insert(s);
        unordered_map<string, int> hash;
        for(char c : paragraph){
            if(('a' <= c && c <= 'z') || ('A' <= c && c <= 'Z'))
                word += tolower(c);
            else{
                if(word != "" && !bannedword.count(word)){
                    hash[word]++;
                    if(hash[word] > ansfreq){
                        ansfreq = hash[word];
                        ans = word;
                    }
                }
                word = "";
            }
        }
        return ans;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU0MDQwOTIwXX0=
-->