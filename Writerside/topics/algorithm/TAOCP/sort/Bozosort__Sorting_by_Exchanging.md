# Bozosort__Sorting_by_Exchanging

﻿---
#Java program

```java
import java.util.Random;

/**
 * User: >_<
 * Date: 11/12/15
 * Time: 1:04 PM
 */

public class BozoSort {

    public static void random_swap(int[] input, int size){

        Random random = new Random();
        int m = random.nextInt(10000) % size;
        int n = (m+1+random.nextInt(10000)%(size-1)) % size;
        int temp = input[m];
        input[m] = input[n];
        input[n] = temp;

        //Output swapped Keys
        System.out.println("Swapped Ks:");
        for(int j=1; j<=input.length; j++){
            System.out.println(j+":"+input[j-1]);
        }
        System.out.println();
}

    public static void bozo_sort(int[] input, int size){
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
            random_swap(input, size);
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
        bozo_sort(number, number.length);

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

Swapped Ks:
1:503
2:87
3:512
4:61
5:908
6:170
7:426
8:275
9:653
10:897
11:154
12:509
13:612
14:677
15:765
16:703

Swapped Ks:
1:503
2:87
3:908
4:61
5:512
6:170
7:426
8:275
9:653
10:897
11:154
12:509
13:612
14:677
15:765
16:703

Swapped Ks:
1:503
2:87
3:154
4:61
5:512
6:170
7:426
8:275
9:653
10:897
11:908
12:509
13:612
14:677
15:765
16:703

......
```

---
#Reference
https://en.wikipedia.org/wiki/Bogosort
