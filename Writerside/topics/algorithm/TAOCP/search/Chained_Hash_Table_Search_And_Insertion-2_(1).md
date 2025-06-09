# Chained_Hash_Table_Search_And_Insertion-2_(1)

﻿#Separate chaining
![Chained Hash Table Search And Insertion-2:Searching](https://img-blog.csdn.net/20151106160051489)

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.


**Node.java**
```java
package com.algorithms.searching;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/13/13
 * Time: 6:52 PM
 * :)~
 * Chained Hash Table Search And Insertion-2:Searching
 */
public class Node {
    int KEY;
    Node LINK;
    Node(int key){
        KEY = key;
        LINK=null;
    }
}
```

**Main.java**
```java
package com.algorithms.searching;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/13/13
 * Time: 6:52 PM
 * :)~
 * Chained Hash Table Search And Insertion-2:Searching
 */
public class Main {

    public static Node[] HEAD = new Node[20];
    public static int M = 19;
    public static int R = M+1;

    public static void searchAndInsertNode(int key){
        int hash = key%19+1;                       /*Hash function:h(K)*/
        Node pointer;

        if(HEAD[hash] == null){
            Node node = new Node(key);
            HEAD[hash] = node;
            System.out.println(String.format("%4s",key+":")+" not found in the hash table, then insert it in HEAD["+hash+"] list");
        }else {
            pointer = HEAD[hash];
            do{
                if(key == pointer.KEY){
                    System.out.println(key+" found in the hash table: HEAD["+hash+"]");
                    break;
                }
                if(pointer.LINK != null){
                    pointer = pointer.LINK;
                }else {
                    Node node = new Node(key);
                    pointer.LINK = node;
                    System.out.println(String.format("%4s",key+":")+" not found in the hash table, then insert it in HEAD["+hash+"] list");
                    break;
                }
            }while (true);
        }
    }

    public static void main(String[] args) {

        /*Prepare the Hash Table*/
        System.out.println("Prepare the Hash Table:");
        searchAndInsertNode(503);
        searchAndInsertNode(87);
        searchAndInsertNode(512);
        searchAndInsertNode(61);
        searchAndInsertNode(908);
        searchAndInsertNode(170);
        searchAndInsertNode(897);
        searchAndInsertNode(275);
        searchAndInsertNode(653);
        searchAndInsertNode(426);
        searchAndInsertNode(154);
        searchAndInsertNode(509);
        searchAndInsertNode(612);
        searchAndInsertNode(677);
        searchAndInsertNode(765);
        searchAndInsertNode(703);
        System.out.println();

        /*Print the current Hash Table with 16 nodes*/
        System.out.println("Print the current Hash Table with 16 nodes:");
        for(int j=1; j<=19; j++){
            Node point = HEAD[j];
            if(point != null){
                System.out.print(String.format("%3s", j+":")+String.format("%4s", point.KEY));
                point = point.LINK;
                while (point != null){
                    System.out.print(" ->"+String.format("%4s", point.KEY));
                    point = point.LINK;
                }
                System.out.println();
            }
        }
        System.out.println();

        /*Search Node 765 in current Hash Table*/
        System.out.println("Search Node 765 in current Hash Table:");
        searchAndInsertNode(765);
        System.out.println();

        searchAndInsertNode(1);
        searchAndInsertNode(2);
        searchAndInsertNode(3);
        searchAndInsertNode(4);
        searchAndInsertNode(5);
    }
}
```

---
#Outputs
```
Prepare the Hash Table:
503: not found in the hash table, then insert it in HEAD[10] list
 87: not found in the hash table, then insert it in HEAD[12] list
512: not found in the hash table, then insert it in HEAD[19] list
 61: not found in the hash table, then insert it in HEAD[5] list
908: not found in the hash table, then insert it in HEAD[16] list
170: not found in the hash table, then insert it in HEAD[19] list
897: not found in the hash table, then insert it in HEAD[5] list
275: not found in the hash table, then insert it in HEAD[10] list
653: not found in the hash table, then insert it in HEAD[8] list
426: not found in the hash table, then insert it in HEAD[9] list
154: not found in the hash table, then insert it in HEAD[3] list
509: not found in the hash table, then insert it in HEAD[16] list
612: not found in the hash table, then insert it in HEAD[5] list
677: not found in the hash table, then insert it in HEAD[13] list
765: not found in the hash table, then insert it in HEAD[6] list
703: not found in the hash table, then insert it in HEAD[1] list

Print the current Hash Table with 16 nodes:
 1: 703
 3: 154
 5:  61 -> 897 -> 612
 6: 765
 8: 653
 9: 426
10: 503 -> 275
12:  87
13: 677
16: 908 -> 509
19: 512 -> 170

Search Node 765 in current Hash Table:
765 found in the hash table: HEAD[6]

  1: not found in the hash table, then insert it in HEAD[2] list
  2: not found in the hash table, then insert it in HEAD[3] list
  3: not found in the hash table, then insert it in HEAD[4] list
  4: not found in the hash table, then insert it in HEAD[5] list
  5: not found in the hash table, then insert it in HEAD[6] list
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
  
