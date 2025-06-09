# Stooge_sort__Sorting_by_Exchanging

﻿#Stooge sort
---
##Animation
![stooge sort](https://img-blog.csdn.net/20151112185804540)
Visualization of Stooge sort.

---
##Complexity

Class					|	Sorting algorithm
------						|	----
Data structure 				|	Array
Worst case performance 		|	$O(n^{\log3 / \log1.5})$
Worst case space complexity	|	$O(n)$


---
#Java program

```java
/**
 * User: >_<
 * Date: 11/12/15
 * Time: 11:19 AM
 */

public class StoogeSort {

    public static void stooge_sort(int[] input, int i, int j){

        if(input[j] < input[i]){
            int temp = input[i];
            input[i] = input[j];
            input[j] = temp;
        }
        if((j-i+1) > 2){
            int t = (j-i+1) / 3;
            stooge_sort(input, i, j-t);
            stooge_sort(input, i+t, j);
            stooge_sort(input, i, j-t);
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
        stooge_sort(number, 0, number.length-1);

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
https://en.wikipedia.org/wiki/Stooge_sort
