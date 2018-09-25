# Sort by bitCount

给一个数组， 按二进制中1的个数进行排序， 如果个数相同再比大小

```java
public static void main(String[] args)
	{
		Integer[] arr = new Integer[]{1,2,3,4,5,6,7};
		Arrays.sort(arr, new Comparator<Integer>(){
			@Override
			public int compare(Integer o1, Integer o2)
			{
				int c1 = Integer.bitCount(o1);
				int c2 = Integer.bitCount(o2);
				if(c1 != c2)
				{
					return Integer.compare(c1, c2);
				}else
				return Integer.compare(o1,o2);
			}
		});
		System.out.println(Arrays.toString(arr));
	}
```

