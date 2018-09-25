# Shift String

 We define the following operations on a string: 

-Left Shift: abcde -&gt; bcdea  Right Shift: abcde -&gt; eabcd 

Complete the function getShiftedString. The function must return the string s after performing several left shifts and right shifts.

left shift:

```java
public static String cyclicLeftShift(String s, int k){
    k = k%s.length();
    return s.substring(k) + s.substring(0, k);
}

public static void main(String[] args)
{
    String test = "Hello World";
    for(int i = 0; i < test.length()*3; i++)
        System.out.println(cyclicLeftShift(test, i));
}


```

![](../.gitbook/assets/image.png)

