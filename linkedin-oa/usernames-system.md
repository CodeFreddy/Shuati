# Usernames System

![](../.gitbook/assets/image%20%2814%29.png)

```java
 // usernamse system

    public static List<String> usernameSystem(List<String> arr)
    {
        List<String> res = new ArrayList<>();
        HashMap<String, Integer> map = new HashMap<>();
        for(String name: arr)
        {
            if(map.containsKey(name))
            {
                int freq = map.get(name);
                StringBuilder temp = new StringBuilder(name);
                temp.append(freq);
                res.add(temp.toString());
                map.put(name, freq + 1);
            }else
            {
                map.put(name, 1);
                res.add(new String(name));
            }
        }
        return res;

    }


    public static void main(String[] args)
    {
        List<String> names = new ArrayList<>();
        names.add("bob");
        names.add("alice");
        names.add("bob");
        names.add("bob");
        names.add("alice");
        List<String> res = usernameSystem(names);
        for(String name: res)
        {
            System.out.println(name);
        }
    }
```

