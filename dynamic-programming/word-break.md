# Word Break



Given a **non-empty** string _s_ and a dictionary _wordDict_ containing a list of **non-empty** words, determine if _s_ can be segmented into a space-separated sequence of one or more dictionary words.

**Note:**

* The same word in the dictionary may be reused multiple times in the segmentation.
* You may assume the dictionary does not contain duplicate words.

**Example 1:**

```text
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

**Example 2:**

```text
Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
```

**Example 3:**

```text
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```



这题的最优子结构在于：

假设字符串lookforthebestworld，用dp\[\]数组记录到某一位为止是否是validWords，则dp\[0\]-dp\[3\]都是false，dp\[4\]是true因为出现了第一个单词look！！！只有此时，才继续判断后续字符串forthebestworld  


```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        if(s.length() == 0) return false;
        
        boolean[] isValid = new boolean[s.length() + 1];
        isValid[0] = true;
        
        for(int i = 1; i <= s.length(); i++)
            for(int j = 0; j < i; j++)
            {
                if(isValid[j] && wordDict.contains(s.substring(j, i)))
                {
                    isValid[i] = true;
                    break;
                }
            }
        return isValid[s.length()];
    }
}
```

