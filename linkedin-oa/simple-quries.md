# simple quries

两个array， 求第一个array里多少个元素小于或者等于第二个array的每一个元素。arr1\[1,4,2,2,6\] arr2\[3,5\] 结果就是\[3, 4\], 暴力解法会超时， 用binary search。

```java
 public static int[] solution(int[] i1, int[] i2) {
        Arrays.sort(i1);
        int[] res = new int[i2.length];
        for(int i = 0; i < i2.length; i++) {
            int temp = bs(i2[i], i1);
            res[i] = temp;
        }
        return res;
    }

    public static int bs(int i, int[] array){
        int left = 0, right = array.length-1;
//        while(left < right) {
//            int mid = left + (right - left) / 2 ;
//            if(array[mid] > i) {
//                right = mid;
//            } else {
//                left = mid + 1;
//            }
//        }
//        return left;
        while(left + 1 < right)
        {
            int mid = left + (right - left) / 2;
            if(array[mid] > i)
                right = mid;
            else
                left = mid;
        }

        if(left <= i) return left + 1;
        else return right + 1;
    }

    public static void main(String args[]) {
        int[] x= new int[]{1,4,2,2,6};
        int[] y= new int[]{3,4};

        int[] res = solution(x,y);
        for(int i = 0; i < res.length; i++) {
            System.out.println("" + res[i]);
        }


    }
```

