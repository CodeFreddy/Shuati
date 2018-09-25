# Minimum Unique array sum



Given a sorted integer array. We need to make array elements distinct by increasing values and keeping array sum minimum possible. We need to print the minimum possible sum as output.

**Examples:**

```text
Input : arr[] = { 2, 2, 3, 5, 6 } ; 
Output : 20
Explanation : We make the array as {2, 
3, 4, 5, 6}. Sum becomes 2 + 3 + 4 + 
5 + 6 = 20

Input : arr[] = { 20, 20 } ; 
Output : 41
Explanation : We make {20, 21}

Input :  arr[] = { 3, 4, 6, 8 };
Output : 21
Explanation : All elements are unique 
so result is sum of each elements.  
```

```java
 static int minSum(int arr[], int n)
    {
        int sum = arr[0], prev = arr[0];
     
        for (int i = 1; i < n; i++) {
     
            // If violation happens, make current
            // value as 1 plus previous value and
            // add to sum.
            if (arr[i] <= prev) {
                prev = prev + 1;
                sum = sum + prev;
            }
     
            // No violation.
             
            else {
                sum = sum + arr[i];
                prev = arr[i];
            }
        }
     
        return sum;
    }
     
    // Drivers code
    public static void main (String[] args) {
     
        int arr[] = { 2, 2, 3, 5, 6 };
        int n = arr.length;
         
        System.out.println(minSum(arr, n));
    }
```

