# Radix_exchange_sort__Sorting_by_Exchanging

﻿#Algorithm R
**Algorithm R** (**Radix exchange sort**). Records R1,... ,RN are rearranged in 
place; after sorting is complete, their keys will be in order, K1 <= ... <= KN. Each 
key is assumed to be a nonnegative m-bit binary number, (a1 a2 ... am)2; the ith 
most significant bit, ai, is called "bit i" of the key. An auxiliary stack with 
room for at most m-1 entries is needed for temporary storage. This algorithm 
essentially follows the radix exchange partitioning procedure described in the 
text above; certain improvements in its efficiency are possible, as described in 
the text and exercises below. 
**R1**. [Initialize.] Set the stack empty, and set I <-- 1, r <-- N, b <-- 1. 
**R2**. [Begin new stage.] (We now wish to sort the subfile Rl ... Rr on bit b; 
from the nature of the algorithm, we have I <= r.) If I = r, go to step R10 
(since a one-word file is already sorted). Otherwise set i <-- I, j <-- r. 
**R3**. [Inspect Ki for 1.] Examine bit b of Ki. If it is a 1, go to step R6. 
**R4**. [Increase i.] Increase i by 1. If i <= j, return to step R3; otherwise go to 
step R8. 
**R5**. [Inspect Kj+1 for 0.] Examine bit b of Kj+1. If it is a 0, go to step R7. 
**R6**. [Decrease j.] Decrease j by 1. If i <= j, go to step R5; otherwise go to 
step R8. 
**R7**. [Exchange Ri, Rj+1] Interchange records Ri <--> Rj+1; then go to step R4. 
**R8**. [Test special cases.] (At this point a partitioning stage has been completed; 
i = j+1, bit b of keys Kl, ... , Kj is 0, and bit b of keys Ki, ... ,Kr is 1.) 
Increase b by 1. If b > m, where m is the total number of bits in the keys, 
go to step R10. (In such a case, the subfile Rl ... Rr has been sorted. This 
test need not be made if there is no chance of having equal keys present in 
the file.) Otherwise if j < I or j = r, go back to step R2 (all bits examined 
were 1 or 0, respectively). Otherwise if j = I, increase I by 1 and go to 
step R2 (there was only one 0 bit). 
**R9**. [Put on stack.] Insert the entry (r, b) on top of the stack; then set r <-- j 
and go to step R2. 
**R10**. [Take off stack.] If the stack is empty, we are done sorting; otherwise set 
I <-- r+1, remove the top entry (r', b') of the stack, set r <-- r', b <-- b', and 
return to step R2. **|** 

---
#Data table
![这里写图片描述](https://img-blog.csdn.net/20151106154254230)

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/4/13
 * Time: 10:01 PM
 * :)~
 * Radix exchange sort:Sorting by Exchanging:Internal Sorting
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        String[] K = new String[17];
        int m = 10;                       /*Total number of bits in the Ks*/
        int[] R = new int[10];            /*At most m-1*/
        int[] B = new int[10];            /*At most m-1*/

        /*Prepare the input data*/
        K[1] = Integer.toBinaryString(503);
        K[2] = Integer.toBinaryString(87);
        K[3] = Integer.toBinaryString(512);
        K[4] = Integer.toBinaryString(61);
        K[5] = Integer.toBinaryString(908);
        K[6] = Integer.toBinaryString(170);
        K[7] = Integer.toBinaryString(897);
        K[8] = Integer.toBinaryString(275);
        K[9] = Integer.toBinaryString(653);
        K[10] = Integer.toBinaryString(426);
        K[11] = Integer.toBinaryString(154);
        K[12] = Integer.toBinaryString(509);
        K[13] = Integer.toBinaryString(612);
        K[14] = Integer.toBinaryString(677);
        K[15] = Integer.toBinaryString(765);
        K[16] = Integer.toBinaryString(703);

    /*Transform Decimal to Binary(all 10bits in this example) and output unsorted Ks*/
        System.out.println("Unsorted Ks:");
        for(int i=1; i<=N; i++){
            if(K[i].length() < 10){
                switch (10 - K[i].length()){
                    case 1: K[i] = "0" + K[i]; break;
                    case 2: K[i] = "00" + K[i]; break;
                    case 3: K[i] = "000" + K[i]; break;
                    case 4: K[i] = "0000" + K[i]; break;
                    case 5: K[i] = "00000" + K[i]; break;
                    case 6: K[i] = "000000" + K[i]; break;
                    case 7: K[i] = "0000000" + K[i]; break;
                    case 8: K[i] = "00000000" + K[i]; break;
                    case 9: K[i] = "000000000" + K[i]; break;
                }
            }
            System.out.println(String.format("%3s", i+":")+String.format("%11s", K[i])+":"+Integer.parseInt(K[i], 2));
        }
        System.out.println();

        /*Kernel of the Algorithm!*/
        int l = 1;                              /*R1*/
        int r = N;
        int b = 1;
        int len = 0;
        int i;
        int j;
        String temp;

        do{
            do{
                if(l == r){                          /*R2*/
                    break;
                }else {
                    i = l;
                    j = r;
                }
                do{
                    if(K[i].charAt(b-1) == '1'){        /*R3*/
                        do{
                            j--;                            /*R6*/
                            if(i <= j){
                                if(K[j+1].charAt(b-1) == '0'){   /*R5*/
                                    temp = K[i];                /*R7*/
                                    K[i] = K[j+1];
                                    K[j+1] = temp;
                                    break;
                                }
                            }else {
                                break;
                            }
                        }while (true);
                        if(i > j){
                            break;
                        }
                    }
                        i++;                   /*R4*/
                        if(i <= j){
                            /*Go to R3*/
                        }else {
                            break;/*Go to R8*/
                        }
                }while (true);
                b++;                         /*R8*/
                if(b > m){
                    break;
                }else if(j < l || j == r){
                    /*Go to R2*/
                }else if(j == l){
                    l++;
                    /*Go to R2*/
                }else {
                    len++;
                    R[len] = r;             /*R9*/
                    B[len] = b;
                    r = j;
                }
            }while (true);
            if(len == 0){             /*R10*/
                break;
            }else {
                l = r+1;
                r = R[len];
                b = B[len];
                len--;
            }
        }while (true);

        /*Output sorted Ks*/
        System.out.println("Sorted Ks:");
        for(i=1; i<=N; i++){
            System.out.println(String.format("%3s", i+":")+String.format("%11s", K[i])+":"+Integer.parseInt(K[i], 2));   /*Transform Binary to Decimal*/
        }
    }
}
```

---
#Outputs
```
Unsorted Ks:
 1: 0111110111:503
 2: 0001010111:87
 3: 1000000000:512
 4: 0000111101:61
 5: 1110001100:908
 6: 0010101010:170
 7: 1110000001:897
 8: 0100010011:275
 9: 1010001101:653
10: 0110101010:426
11: 0010011010:154
12: 0111111101:509
13: 1001100100:612
14: 1010100101:677
15: 1011111101:765
16: 1010111111:703

Sorted Ks:
 1: 0000111101:61
 2: 0001010111:87
 3: 0010011010:154
 4: 0010101010:170
 5: 0100010011:275
 6: 0110101010:426
 7: 0111110111:503
 8: 0111111101:509
 9: 1000000000:512
10: 1001100100:612
11: 1010001101:653
12: 1010100101:677
13: 1010111111:703
14: 1011111101:765
15: 1110000001:897
16: 1110001100:908
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
