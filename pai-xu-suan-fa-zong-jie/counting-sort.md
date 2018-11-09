# Counting Sort

{% embed url="https://www.geeksforgeeks.org/counting-sort/" %}

```java
public class CountingSort {
    public void sort(char[] arr)
    {
        int n = arr.length;
        char[] output = new char[n];
        int[] count = new int[256];

        for(int i = 0; i < n; i++)
        {
            count[arr[i]]++;
        }

        for(int i = 1; i < 256; i++)
            count[i] += count[i-1];

        for(int i = n - 1; i >= 0; i--)
        {
            output[count[arr[i]] - 1] = arr[i];
            --count[arr[i]];
        }

        // Copy the output array to arr, so that arr now
        // contains sorted characters
        for (int i = 0; i<n; ++i)
            arr[i] = output[i];
    }
    // Driver method
    public static void main(String args[])
    {
        CountingSort ob = new CountingSort();
        char arr[] = {'g', 'e', 'e', 'k', 's', 'f', 'o',
                'r', 'g', 'e', 'e', 'k', 's'
        };

        ob.sort(arr);

        System.out.print("Sorted character array is ");
        for (int i=0; i<arr.length; ++i)
            System.out.print(arr[i]);
    }
}

```

时间复杂度:

**Time Complexity:** O\(n+k\) where n is the number of elements in input array and k is the range of input.  
**Auxiliary Space:** O\(n+k\)

**Points to be noted:**  
**1.** Counting sort is efficient if the range of input data is not significantly greater than the number of objects to be sorted. Consider the situation where the input sequence is between range 1 to 10K and the data is 10, 5, 10K, 5K.  
**2.** It is not a comparison based sorting. It running time complexity is O\(n\) with space proportional to the range of data.  
**3.** It is often used as a sub-routine to another sorting algorithm like radix sort.  
**4.** Counting sort uses a partial hashing to count the occurrence of the data object in O\(1\).  
**5.** Counting sort can be extended to work for negative inputs also.

