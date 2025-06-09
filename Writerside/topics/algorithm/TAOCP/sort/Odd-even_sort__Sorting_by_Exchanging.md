# Odd-even_sort__Sorting_by_Exchanging

﻿#Odd-even sort:奇偶排序

---
##Animation
![odd even sort](https://img-blog.csdn.net/20151112192903535)
![odd_even_sort.png](odd_even_sort.png)
Example of odd-even transposition sort sorting a list of random numbers

---
##Complexity

Class					|	Sorting algorithm
------						|	----
Data structure 				|	Array
Worst case performance 		|	$O(n^2)$
Best case performance 		|	$O(n)$
Worst case space complexity	|	$O(1)$


---
#Java program

```java
/**
 * User: >_<
 * Date: 11/10/15
 * Time: 7:51 PM
 */

public class OddEvenSort {

    private static void odd_even_sort(int arr[]) {
        int len = arr.length;
        int odd_even, i;
        int temp;
        int sorted = 0;
        while (sorted == 0) {
            sorted = 1;
            for (odd_even = 0; odd_even < 2; odd_even++)
                for (i = odd_even; i < len - 1; i += 2)
                    if (arr[i] > arr[i+1]) {
                        temp = arr[i];
                        arr[i] = arr[i+1];
                        arr[i + 1] = temp;
                        sorted = 0;
                    }
        }
    }

    public static void main(String[] args) {

        //Prepare the data
        int[] number = {503,87,512,61,908,170,897,275,653,426,154,509,612,677,765,703};

        //Output unsorted Keys
        System.out.println("Unsorted Ks:");
        for(int i=1; i<=number.length; i++){
            System.out.println(i+":"+number[i-1]);
        }
        System.out.println();

        //Kernel of the Algorithm!
        odd_even_sort(number);

        //Output sorted Keys
        System.out.println("Sorted Ks:");
        for(int i=1; i<=number.length; i++){
            System.out.println(i+":"+number[i-1]);
        }

    }
}

```

---
#Outputs
```
Unsorted Ks:
1:503
2:87
3:512
4:61
5:908
6:170
7:897
8:275
9:653
10:426
11:154
12:509
13:612
14:677
15:765
16:703

Sorted Ks:
1:61
2:87
3:154
4:170
5:275
6:426
7:503
8:509
9:512
10:612
11:653
12:677
13:703
14:765
15:897
16:908
```
