# Bulls and Cows

You are playing the following [Bulls and Cows](https://en.wikipedia.org/wiki/Bulls_and_Cows) game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position \(called "bulls"\) and how many digits match the secret number but locate in the wrong position \(called "cows"\). Your friend will use successive guesses and hints to eventually derive the secret number.

Write a function to return a hint according to the secret number and friend's guess, use `A` to indicate the bulls and `B` to indicate the cows. 

Please note that both secret number and friend's guess may contain duplicate digits.

**Example 1:**

```text
Input: secret = "1807", guess = "7810"

Output: "1A3B"

Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.
```

**Example 2:**

```text
Input: secret = "1123", guess = "0111"

Output: "1A1B"

Explanation: The 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow.
```

**Note:** You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.



解题思路：

数字只能是0 - 9， 那么新建一个大小为10的数组， 相应的index对应得就是该数字出线的次数。遍历secret， 如果secret.charAt\(i\) == guess.chaAt\(i\)， 就说明是数字和位置一样， bulls加1。 如果不一样，在数组中secret该位置的值为负数， 说明该数字在guess中出现过了。 那么cows++然后该位置自增1。 guess也一样，只不过是如果此时位置大于0，说明该数字在secret中出现过。cows++，然后自减1。

```java
class Solution {
    public String getHint(String secret, String guess) {
        int bulls = 0;
        int cows = 0;
        int[] numbers = new int[10];
        for(int i = 0; i < secret.length(); i++)
        {
            if(secret.charAt(i) == guess.charAt(i))
            {
                bulls++;
            }else
            {
                if(numbers[secret.charAt(i) - '0']++ < 0) cows++;
                if(numbers[guess.charAt(i) - '0']-- > 0) cows++;
            }
        }
        
        return bulls + "A" + cows + "B";
    }
}
```

