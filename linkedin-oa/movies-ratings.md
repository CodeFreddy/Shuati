# Movies Ratings

求子序列最大和,最多允许跳过一个连续的元素,不能一次跳两个以上,比如【9,-1,-3,5,6】输出19

```java
// movie rating

public static int movieRating(int[] arr)
{
	int takeCur = arr[0], doNotTake = 0;
	for(int i = 1; i < arr.length; i++)
	{
		int temp = doNotTake;
		doNotTake = takeCur;
		takeCur = Math.max(temp, takeCur) + arr[i];
	}

	return Math.max(doNotTake, takeCur);
}

public static void main(String[] args)
{
	int[] arr = new int[]{9, -1, -3, 5, 6};
	System.out.println(movieRating(arr));
}
```

