# H Index

Given an array of citations \(each citation is a non-negative integer\) of a researcher, write a function to compute the researcher's h-index.

According to the [definition of h-index on Wikipedia](https://en.wikipedia.org/wiki/H-index): "A scientist has index h if h of his/her N papers have **at least** h citations each, and the other N − h papers have **no more than** h citations each."

**Example:**

```text
Input: citations = [3,0,6,1,5]
Output: 3 
Explanation: [3,0,6,1,5] means the researcher has 5 papers in total and each of them had 
             received 3, 0, 6, 1, 5 citations respectively. 
             Since the researcher has 3 papers with at least 3 citations each and the remaining 
             two with no more than 3 citations each, her h-index is 3.
```

**Note:** If there are several possible values for _h_, the maximum one is taken as the h-index.

解题思路：

看懂题意， 找到h篇paper，citation都不低于h。剩下的N - h的citation都小于h。首先，h值肯定不可能大于array的长度。 然后新建一个数组， 长度是n+1。 这样index对应位置的值就是相应citation数的文章的数量。 比如index=3，就表示citation为3的文章有多少篇。 如果citation的值大于n， 那将这些文章数量都存入arr\[n\]里。最后再从高到底， total是存的文章总数， 如果total的数量大于某个index，说明已经找到题目所需要的答案了。因为这些paper的citation都高于或等于该citation。此时不需要再继续，因为这是能找到的最大index。

```java
class Solution {
    public int hIndex(int[] citations) {
        int n = citations.length;
        if(n == 0) return 0;
        
        int total = 0;
        int[] arr = new int[n + 1];
        for(int i = 0; i < n; i++)
        {
            if(citations[i] >= n) arr[n]++;
            else
                arr[citations[i]]++;
        }
        
        for(int i = n; i > 0; i--)
        {
            total += arr[i];
            if(total >= i)
                return i;
        }
        
        return 0;
    }
}
```

