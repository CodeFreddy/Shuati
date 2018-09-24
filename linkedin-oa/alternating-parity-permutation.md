# Alternating parity permutation

输入n， 返回 1 - n 的所有permutation， 但是要求是相邻两个数的奇偶性不同。 并且permutation按照字典序大小输出

n = 3 符合条件的有 \[1,2,3\] \[3,2,1\] n = 4 符合条件的有8个



```java
public class Main{
	private static void dfs(int n, List<List<Integer>> res, List<Integer> cur)
	{
		if(cur.size() == n)
		{
			res.add(new ArrayList<>(cur));
		}

		for(int i = 1; i <= n; i++)
		{
			if(cur.contains(i))
				continue;

			if(cur.get(cur.size() - 1) % 2 + (i%2) != 1)
				continue;

			cur.add(i);
			dfs(n, res, cur);
			cur.remove(cur.size() - 1);
		}
	}

	public static void main(String[] args)
	{
		int n = 4;

		List<List<Integer>> res = new ArrayList<>();
		if(n == 0)
		{
			System.out.println("null");
		}
		dfs(n, res, new ArrayList<Integer>());
		Collections.sort(res);
		for(List<Integer> innerList: res)
		{
			System.out.println(innerList);
		}
		
			
	}
}
```

以上代码还没有对res里的arraylist进行字典排序

