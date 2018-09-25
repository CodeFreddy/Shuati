# Last Substring

 Given the string "ab", we find the alphabetically-ordered set of its substrings to be {"a", "ab", "b"}. The substring that occurs last in the ordered list is "b". This is the value to determine.

 思路：  
先遍歷 string 找到最大的 char，再遍歷一次 string，依序取出以最大 char 開頭的 substring，並利用 s1.compareTo\(s2\) &gt; 0 判斷 s1 是否大於 s2。

```java
public static String lastSubstring(String a) {
        List<String> res = new ArrayList<>();
        char maxChar = 'a';
        char[] sc = a.toCharArray();
        for(int i = 0; i < sc.length; i++) {
            if(sc[i] > maxChar) {
                maxChar = sc[i];
                res.clear();
                res.add(a.substring(i));
            } else if(sc[i] == maxChar) {
                res.add(a.substring(i));
            }
        }
        Collections.sort(res);
        return res.get(res.size()-1);
    }

    public static void main(String[] args)
    {
        String str = new String("ab");
        System.out.println(lastSubstring(str));
    }
```

