# Palindrome Partitioning



Given a string _s_, partition _s_ such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of _s_.

**Example:**

```text
Input: "aab"
Output:
[
  ["aa","b"],
  ["a","a","b"]
]
```

 这又是一道需要用DFS来解的题目，既然题目要求找到所有可能拆分成回文数的情况，那么肯定是所有的情况都要遍历到，对于每一个子字符串都要分别判断一次是不是回文数，那么肯定有一个判断回文数的子函数，还需要一个DFS函数用来递归，再加上原本的这个函数，总共需要三个函数来求解。代码如下：

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new LinkedList<List<String>>();
        List<String> out = new LinkedList<String>();
        DFS(res, out, s, 0);
        return res;
        
    }
    
    public void DFS(List<List<String>> res, List<String> out, String s, int start){
        if(start == s.length())
        {
             res.add(new LinkedList(out));
             return;
        }
        
        for(int i = start; i < s.length(); i++)
        {
            if(isValidPalindrome(s, start, i))
            {
                out.add(s.substring(start, i+1));
                DFS(res, out, s, i + 1);
                out.remove(out.size() - 1);
            }
        }
    }
    
    public boolean isValidPalindrome(String s, int start, int end)
    {
        while(start < end)
        {
            if(s.charAt(start) != s.charAt(end)) return false;
            start++;
            end--;
        }
        
        return true;
    }
}
```

