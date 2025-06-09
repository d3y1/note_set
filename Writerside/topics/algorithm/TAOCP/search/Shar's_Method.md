# Shar's_Method

﻿#Comparison tree
![Shar's Method:Searching](https://img-blog.csdn.net/20151106155442398)

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
 * Shar's Method:Searching
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[18];

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
        K[17] = 10000;                /*Positive Infinite*/
        int k = (int)Math.floor(Math.log(N)/Math.log(2));
        int i = (int)Math.pow(2, k);
        int delta = (int)Math.pow(2, k);
        int l = (int)Math.ceil(Math.log(N-Math.pow(2, k)+1)/Math.log(2));

        if(Key > K[i]){
            delta = (int)Math.pow(2, l);
            i = N+1-(int)Math.pow(2, l);
            i = i+(int)Math.ceil((double)delta/2);
            delta = (int)Math.floor((double)delta/2);
        }

        do{
            if(Key < K[i]){
                if(delta == 0){
                    System.out.println("Outputs: "+Key+" not found.");
                    break;
                }else {
                    i = i-(int)Math.ceil((double)delta/2);
                    delta = (int)Math.floor((double)delta/2);
                }
            }else if(Key > K[i]){
                if(delta == 0){
                    System.out.println("Outputs: "+Key+" not found.");
                    break;
                }else {
                    i = i+(int)Math.ceil((double)delta/2);
                    delta = (int)Math.floor((double)delta/2);
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
