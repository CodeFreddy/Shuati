# Find the Celebrity

#### Description

Suppose you are at a party with `n` people \(labeled from `0` to `n - 1`\) and among them, there may exist one celebrity. The definition of a celebrity is that all the other `n - 1` people know him/her but he/she does not know any of them.

Now you want to find out who the celebrity is or verify that there is not one. The only thing you are allowed to do is to ask questions like: "Hi, A. Do you know B?" to get information of whether A knows B. You need to find out the celebrity \(or verify there is not one\) by asking as few questions as possible \(in the asymptotic sense\).

You are given a helper function `bool knows(a, b)` which tells you whether A knows B. Implement a function `int findCelebrity(n)`, your function should minimize the number of calls to `knows`.

解题思路：

这道题首先要理清题意，要找名人， 名人是别的所有人都认识他， 但是他不认识任何一个其他人。那么如果完全不会，可以用暴力解法，对于每一个人 都去调用know函数，去判断他和其他人是否认识，和其他人是否认识他。这样的话时间复杂度是O\(n^2\)。 这显然不是最好的答案。这里题目的关键信息是：如果know\(i,j\)成立，说明一个问题， i肯定不是名人，因为名人不认识任何一个人。 那如果know\(i,j\)不成立，说明j肯定不是名人，因为名人每个人都认识他。这样就可以把时间复杂度变成O\(n\)了。

分两步来：1。 遍历一遍array， 从0 - n -1， 设置一个candidate变量， 如果know\(candidate, i\)为真， 那么candidate往后移动， 否则不处理，因为i不是所想找的人 直接跳过 加1。 这样选出可能是答案的人选，但至少可能。因为这部操作只判断了candidate不认识右边的人， 但是不知道candidate右边的人是不是都认识他， 所以需要再遍历一次。

2。 从头开始遍历， 如果know\(candidate, i\)或者 !know\(i, candidate\)（i不认识candidate， 那么candidate肯定不是名人）那么说明candidate都不是答案，直接返回-1。 到最后 都满足 那就说明candidate是要找的人

```java
/* The knows API is defined in the parent class Relation.
      boolean knows(int a, int b); */

public class Solution extends Relation {
    /**
     * @param n a party with n people
     * @return the celebrity's label or -1
     */
    public int findCelebrity(int n) {
        // Write your code here
        int candidate = 0;
        for(int i = 1; i < n; i++)
        {
            if(knows(candidate, i))
                candidate = i;
            
                
        }
        
        for(int i = 0; i < n; i++)
        {
            if(i == candidate) continue;
            if(!knows(i, candidate) || knows(candidate, i))
                return -1;
        }
        return candidate;
    }
}
```

