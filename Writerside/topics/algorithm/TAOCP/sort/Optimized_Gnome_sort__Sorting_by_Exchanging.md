# Optimized_Gnome_sort__Sorting_by_Exchanging

﻿---
#Java program

```java
/**
 * User: >_<
 * Date: 11/12/15
 * Time: 10:51 AM
 */

public class OptimizedGnomeSort {

    public static void optimized_gnome_sort(int[] input){
        int pos = 1;
        int last = 0;
        while (pos < input.length){
            if(input[pos] >= input[pos-1]){
                if(last != 0){
                    pos = last;
                    last = 0;
                }
                pos++;
            }
            else{
                int temp = input[pos];
                input[pos] = input[pos-1];
                input[pos-1] = temp;
                if(pos > 1){
                    if(last == 0)
                        last = pos;
                    pos--;
                }else{
                    pos++;
                }
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
        optimized_gnome_sort(number);

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
