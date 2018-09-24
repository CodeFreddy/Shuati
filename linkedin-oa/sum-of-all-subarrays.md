# Sum of all Subarrays



Given an integer array ‘arr\[\]’ of size n, find sum of all sub-arrays of given array.

**Examples :**

```text
Input   : arr[] = {1, 2, 3}
Output  : 20
Explanation : {1} + {2} + {3} + {2 + 3} + 
              {1 + 2} + {1 + 2 + 3} = 20

Input  : arr[] = {1, 2, 3, 4}
Output : 50
```

```java
 public static long SubArraySum(int arr[], int n) 
    { 
        long result = 0; 
       
        // Pick starting point 
        for (int i = 0; i < n; i ++) 
        { 
            // Pick ending point 
            for (int j = i; j < n; j ++) 
            { 
                // sum subarray between current 
                // starting and ending points 
                for (int k = i; k <= j; k++) 
                    result += arr[k] ; 
            } 
        } 
        return result ; 
    } 
    
       /* Driver program to test above function */
    public static void main(String[] args)  
    { 
        int arr[] = {1, 2, 3} ; 
        int n = arr.length; 
        System.out.println("Sum of SubArray : " +  
                          SubArraySum(arr, n)); 
    } 

```

 **Time Complexity :** O\(n3\)

参考链接： [https://www.geeksforgeeks.org/sum-of-all-subarrays/](https://www.geeksforgeeks.org/sum-of-all-subarrays/)



