# Shift String

 We define the following operations on a string: 

-Left Shift: abcde -&gt; bcdea  Right Shift: abcde -&gt; eabcd 

Complete the function getShiftedString. The function must return the string s after performing several left shifts and right shifts.

```java
// shift string
    public static String shiftString(String s, int leftShifts, int rightShifts)
    {
        int num = leftShifts - rightShifts;
        if(num == 0) return s;
        // left shift
        if(num > 0)
        {
            int k = num % s.length();
            return s.substring(k) + s.substring(0, k);
        }else
        {
            int k = Math.abs(num) % s.length();
            return s.substring(s.length() - k) + s.substring(0, s.length() - k);
        }
    }

    public static void main(String[] args)
    {
        String str = "abcde";
        System.out.println(shiftString(str, 2, 2));
    }

```

![](../.gitbook/assets/image.png)

