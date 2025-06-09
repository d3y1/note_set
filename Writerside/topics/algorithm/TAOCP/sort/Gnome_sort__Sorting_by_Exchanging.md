# Gnome_sort__Sorting_by_Exchanging

﻿#Gnome sort:地精排序

---
##Animation
![gnome sort](https://img-blog.csdn.net/20151112191428756)
Visualisation of Gnome sort

---
##Complexity

Class						|	Sorting algorithm
------							|	----
Data structure 					|	Array
Worst case performance 			|	$O(n^2)$
Best case performance 			|	$\Omega(n)$
Average case performance 		|	$O(n^2)$
Worst case space complexity		|	$O(1)$ auxiliary


---
#Java program

```java
/**
 * User: >_<
 * Date: 11/12/15
 * Time: 10:41 AM
 */

public class GnomeSort {

    public static void gnome_sort(int[] input){
        int pos = 1;
        while (pos < input.length){
            if(input[pos] >= input[pos-1])
                pos++;
            else{
                int temp = input[pos];
                input[pos] = input[pos-1];
                input[pos-1] = temp;
                if(pos > 1)
                    pos--;
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
        gnome_sort(number);

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
https://en.wikipedia.org/wiki/Gnome_sort
