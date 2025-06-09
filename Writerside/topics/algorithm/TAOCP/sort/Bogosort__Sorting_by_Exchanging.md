# Bogosort__Sorting_by_Exchanging

﻿
#Bogosort

---
##Animation
![single shuffle bogosort](https://img-blog.csdn.net/20151112184715289)
![single_shuffle_bogosort.png](single_shuffle_bogosort.png)
A possible, but improbable, single shuffle execution of the bogo sort algorithm.

---
##Complexity

Class										|	Sorting algorithm
------											|	----
Data structure 							|	Array
Worst case performance 			|	Unbounded
Best case performance 			|	$\theta(n)$
Average case performance 		|	$O((n+1)!)$
Worst case space complexity	|	$O(n)$


---
#Java program

```java
import java.util.Random;

/**
 * User: >_<
 * Date: 11/12/15
 * Time: 12:23 PM
 */

public class BogoSort {

    public static void shuffle(int[] input, int size){
        int i, r, t;
        Random random = new Random();
        for(i=0; i<size-1; i++){
            r = random.nextInt(10000) % (size-i);
            t = input[i];
            input[i] = input[r+i];
            input[r+i] = t;
        }

        //Output shuffled Keys
        System.out.println("Shuffled Ks:");
        for(int j=1; j<=input.length; j++){
            System.out.println(j+":"+input[j-1]);
        }
        System.out.println();
    }

    public static void bogo_sort(int[] input, int size){
        int i;
        int flag;
        while (true){
            flag = 0;
            for(i=0; i<size-1; i++){
                if(input[i] > input[i+1]){
                    flag = 1;
                    break;
                }
            }
            if(flag == 0)
                break;
            shuffle(input, size);
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
        bogo_sort(number, number.length);

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

Shuffled Ks:
1:765
2:897
3:426
4:275
5:612
6:512
7:653
8:87
9:154
10:677
11:908
12:503
13:509
14:61
15:170
16:703

Shuffled Ks:
1:765
2:275
3:87
4:703
5:612
6:154
7:61
8:677
9:908
10:512
11:426
12:503
13:653
14:170
15:509
16:897

Shuffled Ks:
1:653
2:87
3:170
4:703
5:612
6:677
7:897
8:426
9:503
10:908
11:509
12:765
13:512
14:61
15:275
16:154

......
```

---
#Reference
https://en.wikipedia.org/wiki/Bogosort
