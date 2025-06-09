# Uniform_Binary_Search-2

﻿#Algorithm C
**Algorithm C** (**Uniform binary search**). This algorithm is just like Algorithm U, 
but it uses an auxiliary table in place of the calculations involving m. The table 
entries are 
              DELTA[j] = floor((N+2^(j-1))/2^j),        for 1 <= j <= floor(lgN)+2.       (6) 
**C1**. [Initialize.] Set i <-- DELTA[1], j <--2. 
**C2**. [Compare.] If K < Ki, go to C3; if K > Ki, go to C4; and if K = Ki, the 
algorithm terminates successfully. 
**C3**. [Decrease i.] If DELTA[j] = 0, the algorithm terminates unsuccessfully. 
Otherwise, set i <-- i-DELTA[j], j <-- j + 1, and go to C2. 
**C4**. [Increase i.] If DELTA[j] = 0, the algorithm terminates unsuccessfully. 
Otherwise, set i <-- i+DELTA[j] , j <-- j + 1, and go to C2. **|** 

---
#Comparison tree
![Uniform Binary Search-2:Searching](https://img-blog.csdn.net/20151106155214133)

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/11/13
 * Time: 6:52 PM
 * :)~
 * Uniform Binary Search-2:Searching
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[17];

        /*Prepare the ordered data table*/
        K[1] = 61;
        K[2] = 87;
        K[3] = 154;
        K[4] = 170;
        K[5] = 275;
        K[6] = 426;
        K[7] = 503;
        K[8] = 509;
        K[9] = 512;
        K[10] = 612;
        K[11] = 653;
        K[12] = 677;
        K[13] = 703;
        K[14] = 765;
        K[15] = 897;
        K[16] = 908;

        /*Output sorted Ks*/
        System.out.println("Sorted Ks:");
        for(int i=1; i<=N; i++){
            System.out.println(i+":"+K[i]);
        }
        System.out.println();

        /*Kernel of the Algorithm!*/
        int Key = 653;                  /*Key to be found*/
        K[0] = -10000;                /*Negative Infinite*/
        int i = (int)Math.floor((N+Math.pow(2, 1-1))/Math.pow(2, 1));
        int j = 2;
        int deltaJ;

        do{
            deltaJ = (int)Math.floor((N+Math.pow(2, j-1))/Math.pow(2, j));
            if(Key < K[i]){
                if(deltaJ == 0){
                    System.out.println("Outputs: "+Key+" not found.");
                    break;
                }else {
                    i = i-deltaJ;
                    j++;
                }
            }else if(Key > K[i]){
                if(deltaJ == 0){
                    System.out.println("Outputs: "+Key+" not found.");
                    break;
                }else {
                    i = i+deltaJ;
                    j++;
                }
            }else {
                System.out.println("Outputs: "+Key+" in K["+i+"].");
                break;
            }
        }while (true);
    }
}
```

---
#Outputs
```
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

Outputs: 653 in K[11].
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
