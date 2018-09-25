# Untitled

给定一个数组counts， 每个index 代表一个ID， 每个element代表ID所在的组的大小， 组里只能有element这么多个ID， 把element一样的ID归到一个或者多个组里， 按从小到大的顺序输出所有组

举例说明： 0 1 2 3 4 5 6 3 3 3 3 3 1 3

上面一排是index也就是ID 下面一排是ID所在的组的大小

输出结果就是 0 1 2 3 4 6 5

```java
public class Main{
	public static void main(String[] args)
	{
		int[] counts = new int[]{3,3,3,3,3,1,3};

		HashMap<Integer, Integer> map = new HashMap<>();
		List<List<Integer>> result = new ArrayList<>();
		for(int i = 0; i < counts.length; i++)
		{
			int count = counts[i];
			if(!map.containsKey(count))
			{
				List<Integer> tmp = new ArrayList<>();
				tmp.add(i);
				result.add(tmp);
				map.put(count, result.size() - 1);
			}else
			{
				List<Integer> tmp = result.get(map.get(count));
				tmp.add(i);
				if(tmp.size() == count)
				{
					map.remove(count);
				}
			}
		}
		for(List<Integer> list: result)
		{
			System.out.println(list);
		}
	}
}
```

