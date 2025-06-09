# Fibonaccian_Search-1__N+1_is_a_perfect_Fibonacci_number

﻿#Algorithm F
**Algorithm F** (**Fibonaccian search**). Given a table of records R1R2 ... RN whose 
keys are in increasing order K1 < K2 < ... < KN, this algorithm searches for a 
given argument K. 
For convenience in description, we assume that N + 1 is a perfect Fibonacci 
number, Fk+1. It is not difficult to make the method work for arbitrary N, if a 
suitable initialization is provided (see exercise 14). 
**F1**. [Initialize.] Set i <-- Fk, p <-- Fk-1, q <-- Fk-2. (Throughout the algorithm, 
p and q will be consecutive Fibonacci numbers.) 
**F2**. [Compare.] If K < Ki, go to step F3; if K > Ki, go to F4; and if K = Ki, 
the algorithm terminates successfully. 
**F3**. [Decrease i.] If q = 0, the algorithm terminates unsuccessfully. Otherwise 
set i <-- i-q, and set (p, q) <-- (q, p-q); then return to F2. 
**F4**. [Increase i.] If p = 1, the algorithm terminates unsuccessfully. Otherwise 
set i <-- i + q, p <-- p - q, then q <-- q - p, and return to F2. **|** 

---
#Fibonacci tree
![这里写图片描述](https://img-blog.csdn.net/20151106155326701)


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
 * Fibonaccian Search-1:N+1 is a perfect Fibonacci number:Searching
 */
public class Main {

    public static void main(String[] args) {
        int N = 12;
        int[] K = new int[13];

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

        /*Output sorted Ks*/
        System.out.println("Sorted Ks:");
        for(int i=1; i<=N; i++){
            System.out.println(i+":"+K[i]);
        }
        System.out.println();

        /*Kernel of the Algorithm!*/
        int Key = 653;                  /*Key to be found*/
        /*Fibonacci number:0,1,1,2,3,5,8,13,21,34,55...*/
        /*Fn = Fn-1 + Fn-2, F0 = 0, F1 = 1...*/
        /*In this case:N+1=13=F7=Fk+1, then k=6, i=Fk=F6=8, p=Fk-1=F5=5, q=Fk-2=F4=3*/
        int i = 8;
        int p = 5;
        int q = 3;

        do{
            if(Key < K[i]){
                if(q == 0){
                    System.out.println("Outputs: "+Key+" not found.");
                    break;
                }else {
                    i = i-q;
                    int temp = q;
                    q = p-q;
                    p = temp;
                }
            }else if(Key > K[i]){
                if(p == 1){
                    System.out.println("Outputs: "+Key+" not found.");
                    break;
                }else {
                    i = i+q;
                    p = p-q;
                    q = q-p;
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

Outputs: 653 in K[11].
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
