# Can you sort?

sort array by frequency 

\[4,5,6,5,4,3\] -&gt; \[3,6,4,4,5,5\]

```java

public class Main{
	public static void main(String[] args)
	{
		int[] input = new int[]{8, 5,5,5,5,1,1,3,3,4};
		int n = input.length;

		HashMap<Integer, Integer> map = new HashMap<>();
		Integer[] nums = new Integer[n];
		for(int i = 0; i < n; i++)
		{
			nums[i] = new Integer(input[i]);
			map.put(input[i], map.getOrDefault(input[i], 0) + 1);

		}
		Arrays.sort(nums, new Comparator<Integer>()
			{
				@Override
				public int compare(Integer o1, Integer o2){
					Integer c1 = map.get(o1);
					Integer c2 = map.get(o2);
					if(c1 != c2)
					{
						return Integer.compare(c1, c2);
					}else
					{
						return Integer.compare(o1, o2);
					}
				}
			});
		for(Integer num: nums)
		{
			System.out.println(num);
		}
	}
}
```

