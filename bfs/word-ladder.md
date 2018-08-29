# Word Ladder



Given two words \(_beginWord_ and _endWord_\), and a dictionary's word list, find the length of shortest transformation sequence from _beginWord_ to _endWord_, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that _beginWord_ is _not_ a transformed word.

**Note:**

* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume _beginWord_ and _endWord_ are non-empty and are not the same.

**Example 1:**

```text
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```

**Example 2:**

```text
Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```

这是道比较经典的bfs题目， 每次只能更换一个字母，这样的思路是用一个queue，来装所有的可能变化的结果。 比如 hit 的变换，有3\*26种可能性，其实就是要枚举这么多可能性 但是题目规定这样的单词必须在dict里面 所以需要加一个判断条件 如果dict里有这个词才做处理 否则直接continue。 bfs就是一层层的找 所以用queue也是必然的 然后在getNextWord方法里面有一个list用来装与传入的word只相差一个字母的所有可能单词。 



```java
import java.util.*;

public class WordLadder {
    public class Solution {
        /*
         * @param start: a string
         * @param end: a string
         * @param dict: a set of string
         * @return: An integer
         */
        public int ladderLength(String start, String end, Set<String> dict) {
            // write your code here
            if(dict == null)
                return 0;
            if(start.equals(end))
                return 1;

            dict.add(start);
            dict.add(end);
            HashSet<String> hash = new HashSet<>();
            Queue<String>  queue = new LinkedList<>();
            hash.add(start);
            queue.offer(start);

            int length = 1;

            while(!queue.isEmpty())
            {
                length++;

                int size = queue.size();
                for(int i = 0; i < size; i++)
                {
                    String word = queue.poll();
                    for(String nextWord: getNextWord(word, dict))
                    {
                        if(hash.contains(nextWord))
                            continue;
                        if(nextWord.equals(end))
                            return length;

                        hash.add(nextWord);
                        queue.offer(nextWord);
                    }
                }
            }

            return 0;

        }

        public String replace(String word, int index, char c)
        {
            char[] chars = word.toCharArray();
            chars[index] = c;
            return new String(chars);
        }

        public ArrayList<String> getNextWord(String word, Set<String> dict)
        {
            ArrayList<String> nextWords = new ArrayList<>();

            for(char c = 'a'; c <= 'z'; c++)
            {
                for(int i = 0; i < word.length(); i++)
                {
                    if(word.charAt(i) == c)
                        continue;
                    String newWord = replace(word,i, c);
                    if(dict.contains(newWord))
                        nextWords.add(newWord);
                }
            }
            return nextWords;
        }


    }


}
```

 

