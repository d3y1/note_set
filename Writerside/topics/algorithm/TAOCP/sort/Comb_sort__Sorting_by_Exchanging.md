# Comb_sort__Sorting_by_Exchanging

﻿#Comb sort:梳排序

---
##Animation
![comb sort](https://img-blog.csdn.net/20151112192110878)
Visualisation of Comb sort

---
##Complexity

Class					|	Sorting algorithm
------						|	----
Data structure 				|	Array
Worst case performance 		|	$O(n^2)$
Best case performance 		|	$O(n)$
Average case performance 	|	$\Omega(n^2/2^p)$, where p is the number of increments
Worst case space complexity	|	$O(1)$


---
#Java program 1: Using Comparable

```java
/**
 * User: >_<
 * Date: 11/12/15
 * Time: 9:23 AM
 */

public class CombSortUsingComparable {

    public static <E extends Comparable<? super E>> void comb_sort(E[] input) {
        int gap = input.length;
        boolean swapped = true;
        while (gap > 1 || swapped) {
            if (gap > 1) {
                gap = (int) (gap * 0.8);
            }
            int i = 0;
            swapped = false;
            while (i + gap < input.length) {
                if (input[i].compareTo(input[i + gap]) > 0) {
                    E t = input[i];
                    input[i] = input[i + gap];
                    input[i + gap] = t;
                    swapped = true;
                }
                i++;
            }
        }
    }

    public static void main(String[] args) {

        //Prepare the data
        Integer[] number = {503,87,512,61,908,170,897,275,653,426,154,509,612,677,765,703};

        //Output unsorted Keys
        System.out.println("Unsorted Ks:");
        for(int i=1; i<=number.length; i++){
            System.out.println(i+":"+number[i-1]);
        }
        System.out.println();

        //Kernel of the Algorithm!
        comb_sort(number);

        //Output sorted Keys
        System.out.println("Sorted Ks:");
        for(int i=1; i<=number.length; i++){
            System.out.println(i+":"+number[i-1]);
        }

    }
}

```
---
OR

---

#Java program 2
```java
/**
 * User: >_<
 * Date: 11/12/15
 * Time: 9:53 AM
 */

public class CombSort {

    public static void comb_sort(int[] input) {
        int gap = input.length;
        boolean swapped = true;
        while (gap > 1 || swapped) {
            if (gap > 1) {
                gap = (int) (gap * 0.8);
            }
            int i = 0;
            swapped = false;
            while (i + gap < input.length) {
                if (input[i] > input[i + gap]) {
                    int t = input[i];
                    input[i] = input[i + gap];
                    input[i + gap] = t;
                    swapped = true;
                }
                i++;
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
        comb_sort(number);

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

---
#Reference
https://zh.wikipedia.org/wiki/%E6%A2%B3%E6%8E%92%E5%BA%8F
https://en.wikipedia.org/wiki/Comb_sort
