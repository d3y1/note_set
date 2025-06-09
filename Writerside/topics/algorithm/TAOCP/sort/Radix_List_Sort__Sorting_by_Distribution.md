# Radix_List_Sort__Sorting_by_Distribution

﻿#Algorithm R
**Algorithm R** (**Radix list sort**). Records R1,..., RN are each assumed to contain 
a LINK field. Their keys are assumed to be p-tuples 
                                            (a1,a2,...,ap),          0 <= ai < M,                                  (1) 
where the order is defined lexicographically so that 
                                            (a1,a2,...,ap) < (b1,b2,... ,bp)                                        (2) 
if and only if for some j, 1 <= j <= p, we have 
                                         ai = bi        for all i < j,      but        aj < bj.                      (3) 
The keys may, in particular, be thought of as numbers written in radix M 
notation, 
                                      a1M^(p-1) + a2M^(p-2) ... + ap-1M + ap,                          (4) 
and in this case lexicographic order corresponds to the normal ordering of non- 
negative numbers. The keys may also be strings of alphabetic letters, etc. 
      Sorting is done by keeping M "piles" of records, in a manner that exactly 
parallels the action of a card sorting machine. The piles are really queues in the 
sense of Chapter 2, since we link them together so that they are traversed in a 
first-in-first-out manner. There are two pointer variables TOP[i] and BOTM[i] 
for each pile, 0 <= i < M, and we assume as in Chapter 2 that 
                                   LINK(LOC(BOTM[i])) = BOTM[i].                                      (5) 
**R1**. [Loop on k.] In the beginning, set P <-- LOC(RN), a pointer to the last 
record. Then perform steps R2 through R6 for k = 1,2,... ,p. (Steps R2 
through R6 constitute one "pass.") Then the algorithm terminates, with 
P pointing to the record with the smallest key, LINK(P) to the record with 
next smallest, then LINK (LINK (P)), etc.; the LINK in the final record will 
be Null. 
**R2**. [Set piles empty.] Set TOP[i] <-- LOC(BOTM[i]) and BOTM[i] <-- Null, for 
0 <= i < M. 
**R3**. [Extract kth digit of key.] Let KEY(P), the key in the record referenced by P, 
be (a1, a2,..., ap); set i <-- ap+1-k, the kth least significant digit of this key. 
**R4**. [Adjust links.] Set LINK (TOP[i]) <-- P, then set TOP[i] <-- P. 
**R5**. [Step to next record.] If k = 1 (the first pass) and if P = LOC(Rj), for some 
j !=1, set P <-- LOC(Rj-1) and return to R3. If k > 1 (subsequent passes), 
set P <-- LINK(P), and return to R3 if P != Null. 
**R6**. [Do Algorithm H.] (We are now done distributing all elements onto the 
piles.) Perform Algorithm H below, which "hooks together" the individual 
piles into one list, in preparation for the next pass. Then set P <-- BOTM[0], 
a pointer to the first element of the hooked-up list. (See exercise 3.) **|** 

---
#Algorithm H
**Algorithm H** (**Hooking-up of queues**). Given M queues, linked according to 
the conventions of Algorithm R, this algorithm adjusts at most M links so that 
a single queue is created, with BOTM[0] pointing to the first element, and with 
pile 0 preceding pile 1 ... preceding pile M-1. 
**H1**. [Initialize.] Set i <-- 0. 
**H2**. [Point to top of pile.] Set P <-- TOP[i]. 
**H3**. [Next pile.] Increase i by 1. If i = M, set LINK(P) <-- Null and terminate the 
algorithm. 
**H4**. [Is pile empty?] If BOTM[i] = Null, go back to H3. 
**H5**. [Tie piles together.] Set LINK(P) <-- BOTM[i]. Return to H2. **|** 

---
#Flow diagram
![这里写图片描述](https://img-blog.csdn.net/20151106154516740)

---
#Data flow
![这里写图片描述](https://img-blog.csdn.net/20151106154532124)

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.


**Node.java**
```java
package com.algorithms.internal.sorting.distribution;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/8/13
 * Time: 6:52 PM
 * :)~
 * Radix List Sort:Sorting by Distribution:Internal Sorting
 */
public class Node {
    int data;
    Node next;
    Node(int d){
        data = d;
        next=null;
    }
}
```

**List.java**
```java
package com.algorithms.internal.sorting.distribution;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/8/13
 * Time: 5:22 PM
 * :)~
 * Radix List Sort:Sorting by Distribution:Internal Sorting
 */
public class List {
    public Node Head = null;
    private Node Pointer = null;
    private int Length = 0;

    public void insert(int d){
        Node e=new Node(d);
        e.next = Head;
        Head = e;
        Length++;
    }

    public Node current(){
        if(Head == null)
            return null;
        else
            return Head;
    }

    public void printList(){
        Pointer = Head;
        int i = 1;
        while (Pointer != null){
            System.out.println(i+":"+Pointer.data);
            Pointer = Pointer.next;
            i++;
        }
    }
}
```

**Main.java**
```java
package com.algorithms.internal.sorting.distribution;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/8/13
 * Time: 5:22 PM
 * :)~
 * Radix List Sort:Sorting by Distribution:Internal Sorting
 */
public class Main {

    public static void main(String[] args) {
        List K = new List();
        Node[] TOP = new Node[10];
        Node[] BOTM = new Node[10];
        int p = 3;                 /*Decimal bits of each of the Ks to be sorted*/
        int M = 10;                /*Decimal*/

        /*Prepare the data*/
        K.insert(703);
        K.insert(765);
        K.insert(677);
        K.insert(612);
        K.insert(509);
        K.insert(154);
        K.insert(426);
        K.insert(653);
        K.insert(275);
        K.insert(897);
        K.insert(170);
        K.insert(908);
        K.insert(61);
        K.insert(512);
        K.insert(87);
        K.insert(503);

        /*Output unsorted Ks*/
        System.out.println("Unsorted Ks:");
        K.printList();
        System.out.println();

        /*Kernel of the Algorithm!*/
        Node P = null;
        P = K.current();                        /*R1*/
        Node Point = null;

        int Key;

        for(int k=1; k<=p; k++){
            for(int i=0; i<M; i++){
                TOP[i] = BOTM[i] = null;            /*R2*/
            }
            do{
                Key = P.data;                       /*R3*/
                int i = p+1-k;
                switch (i){
                    case 1: i = Key/100; break;
                    case 2: i = (Key/10)%10; break;
                    case 3: i = Key%10; break;
                }

                Point = P;
                if(k == 1){                             /*R4 R5*/
                    if(P.next != null){
                        P = P.next;
                        Point.next = BOTM[i];
                        if(BOTM[i] == null){
                            TOP[i] = BOTM[i] = Point;
                        }else {
                            BOTM[i] = Point;
                        }
                        continue;
                    } else {
                        Point.next = BOTM[i];
                        if(BOTM[i] == null){
                            TOP[i] = BOTM[i] = Point;
                        }else {
                            BOTM[i] = Point;
                        }
                    }
                }else {
                    if(P.next != null){          /*R5*/
                        P = P.next;
                        Point.next = null;
                        if(TOP[i] == null){
                            TOP[i] = BOTM[i] = Point;
                        }else {
                            TOP[i].next = Point;
                            TOP[i] = Point;
                        }
                        continue;
                    } else {
                        Point.next = null;
                        if(TOP[i] == null){
                            TOP[i] = BOTM[i] = Point;
                        }else {
                            TOP[i].next = Point;
                            TOP[i] = Point;
                        }
                    }
                }
                                                         /*R6*/
                int j = 0;                      /*H1*/
                do{
                    P = TOP[j];                     /*H2*/
                    do{
                        j++;                        /*H3*/
                        if(j == M){
                            P.next = null;
                            break;
                        }
                        if(BOTM[j] == null){        /*H4*/

                        }else {
                            P.next = BOTM[j];       /*H5*/
                            break;
                        }
                    }while (true);
                    if(j == M){
                        K.Head = BOTM[0];
                        break;
                    }
                }while (true);
                P = BOTM[0];
                break;
            }while (true);
        }

        /*Output sorted Ks*/
        System.out.println("Sorted Ks:");
        K.printList();
        System.out.println();
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
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
