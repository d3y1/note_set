# Quicksort-1_Sorting_by_Exchanging

﻿#Quicksort-1:快速排序-1

---

##Animation
![quick sort](https://img-blog.csdn.net/20151113122351099)
Animated visualization of the quicksort algorithm. The horizontal lines are pivot values.

---

![这里写图片描述](https://img-blog.csdn.net/20151113122445301)
Full example of quicksort on a random set of numbers. The shaded element is the pivot. It is always chosen as the last element of the partition. However, always choosing the last element in the partition as the pivot in this way results in poor performance ($O(n^2)$) on already sorted arrays, or arrays of identical elements. Since sub-arrays of sorted / identical elements crop up a lot towards the end of a sorting procedure on a large set, versions of the quicksort algorithm which choose the pivot as the middle element run much more quickly than the algorithm described in this diagram on large sets of numbers.

---

##Complexity

Class										|	Sorting algorithm
------											|	----
Data structure 							|	Array
Worst case performance 			|	$O(n^2)$
Best case performance 			|	$O(n \log n)$ (simple partition) or $O(n)$ (three-way partition and equal keys)
Average case performance 		|	$O(n \log n)$
Worst case space complexity	|	$O(n)$ auxiliary (naive), $O(log n)$ auxiliary (Sedgewick 1978)


---

#Pseudo code
```
QUICKSORT(A, p, r)
	if p < r
		q = PARTITION(A, p, r)
		QUICKSORT(A, p, q-1)
		QUICKSORT(A, q+1, r)

PARTITION(A, p, r)
	x = A[r]
	i = p - 1
	for j=p to r-1
		if A[j] <= x
			i = i + 1
			exchange A[i] with A[j]
	exchange A[i+1] with A[r]
	return i+1
```

---
#Java program

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 11/29/13
 * Time: 10:01 PM
 * :)~
 * Quicksort-1:Sorting by Exchanging:Internal Sorting
 */
public class Main {

    public static int PARTITION(int[] K, int p, int r){
        int x = K[r];
        int i = p-1;
        int temp;
        for(int j=p; j<=r-1; j++){
            if(K[j] <= x){
                i++;
                temp = K[i];
                K[i] = K[j];
                K[j] = temp;
            }
        }
        temp = K[i+1];
        K[i+1] = K[r];
        K[r] = temp;
        return i+1;
    }

    public static void QUICKSORT(int[] K, int p, int r){
        if(p < r){
            int q = PARTITION(K, p, r);
            QUICKSORT(K, p, q-1);
            QUICKSORT(K, q+1, r);
        }
    }

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[17];

        /*Prepare the data*/
        K[1] = 503;
        K[2] = 87;
        K[3] = 512;
        K[4] = 61;
        K[5] = 908;
        K[6] = 170;
        K[7] = 897;
        K[8] = 275;
        K[9] = 653;
        K[10] = 426;
        K[11] = 154;
        K[12] = 509;
        K[13] = 612;
        K[14] = 677;
        K[15] = 765;
        K[16] = 703;

        /*Output unsorted Ks*/
        System.out.println("Unsorted Ks:");
        for(int i=1; i<=N; i++){
            System.out.println(i+":"+K[i]);
        }
        System.out.println();

        /*Kernel of the Algorithm!*/
        QUICKSORT(K, 1, N);

        /*Output sorted Ks*/
        System.out.println("Sorted Ks:");
        for(int i=1; i<=N; i++){
            System.out.println(i+":"+K[i]);
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
<< Introduction to Algorithms >> Third Edition, THOMAS H. CORMEN, CHARLES E. LEISERSON, RONALD L. RIVEST, CLIFFORD STEIN.
https://en.wikipedia.org/wiki/Quicksort
