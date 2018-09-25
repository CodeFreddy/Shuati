# Last Substring

 Given the string "ab", we find the alphabetically-ordered set of its substrings to be {"a", "ab", "b"}. The substring that occurs last in the ordered list is "b". This is the value to determine.

 思路：  
先遍歷 string 找到最大的 char，再遍歷一次 string，依序取出以最大 char 開頭的 substring，並利用 s1.compareTo\(s2\) &gt; 0 判斷 s1 是否大於 s2。

