# Tree_Search_And_Insertion

﻿#Algorithm T
**Algorithm T** (**Tree search and insertion**). Given a table of records that form a 
binary tree as described above, this algorithm searches for a given argument K. 
If K is not in the table, a new node containing K is inserted into the tree in the 
appropriate place. 
The nodes of the tree are assumed to contain at least the following fields: 
                      KEY(P) = key stored in NODE(P); 
                   LLINK(P) = pointer to left subtree of NODE (P); 
                  RLINK(P) = pointer to right subtree of NODE(P). 
Null subtrees (the external hodes in Fig. 10) are represented by the null pointer Null. 
The variable ROOT points to the root of the tree. For convenience, we assume 
that the tree is not empty (that is, ROOT != Null), since the necessary operations 
are trivial when ROOT = Null. 
**T1**. [Initialize.] Set P <-- ROOT. (The pointer variable P will move down the tree.) 
**T2**. [Compare.] If K < KEY(P), go to T3; if K > KEY(P), go to T4; and if 
K = KEY(P), the search terminates successfully. 
**T3**. [Move left.] If LLINK(P) != Null, set P <-- LLINK(P) and go back to T2. 
Otherwise go to T5. 
**T4**. [Move right.] If RLINK(P) != Null, set P <-- RLINK(P) and go back to T2. 
**T5**. [Insert into tree.] (The search is unsuccessful; we will now put K into the 
tree.) Set Q <= AVAIL, the address of a new node. Set KEY(Q) <-- K, 
LLINK(Q) <-- RLINK(Q) <-- Null. (In practice, other fields of the new node 
should also be initialized.) If K was less than KEY(P), set LLINK(P) <-- Q, 
otherwise set RLINK(P) <-- Q. (At this point we could set P <-- Q and 
terminate the algorithm successfully.) **|** 

---
#Flow diagram
![这里写图片描述](https://img-blog.csdn.net/20151106155547082)

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.


**Node.java**
```java
package com.algorithms.searching;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/12/13
 * Time: 6:52 PM
 * :)~
 * Tree Search And Insertion:Searching
 */
public class Node {
    int KEY;
    Node LLINK;
    Node RLINK;
    Node(int key){
        KEY = key;
        LLINK=null;
        RLINK=null;
    }
}
```

**Tree.java**
```java
package com.algorithms.searching;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/12/13
 * Time: 5:22 PM
 * :)~
 * Tree Search And Insertion:Searching
 */

public class Tree {
    public Node ROOT = null;
    private int index = 1;

    public void insertNode(Node P, int key){
        Node node = new Node(key);
        node.LLINK = null;
        node.RLINK = null;
        if(ROOT == null){
            ROOT = node;
        }else if(key < P.KEY){
            P.LLINK = node;
        }else if(key > P.KEY){
            P.RLINK = node;
        }
    }

    public void inorderTreePrint(Node root){
        if(root != null){
            inorderTreePrint(root.LLINK);
            System.out.println((index++)+":"+root.KEY);
            inorderTreePrint(root.RLINK);
        }
    }
}
```

**Main.java**
```java
package com.algorithms.searching;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/12/13
 * Time: 6:52 PM
 * :)~
 * Tree Search And Insertion:Searching
 */
public class Main {

    public static Tree tree = new Tree();
    public static int i =1;

    public static void searchAndInsertNode(int key){
        Node P = tree.ROOT;
        if(P == null){
            tree.insertNode(P, key);
            System.out.println(String.format("%2s", i++)+":"+String.format("%4s", key)+": not found in the current tree, and then insert it in the tree.");
        }else {
            do{
                if(key < P.KEY){
                    if(P.LLINK != null){
                        P = P.LLINK;
                    }else {
                        tree.insertNode(P, key);
                        System.out.println(String.format("%2s", i++)+":"+String.format("%4s", key)+": not found in the current tree, and then insert it in the tree.");
                        break;
                    }
                }else if(key > P.KEY){
                    if(P.RLINK != null){
                        P = P.RLINK;
                    }else {
                        tree.insertNode(P, key);
                        System.out.println(String.format("%2s", i++)+":"+String.format("%4s", key)+": not found in the current tree, and then insert it in the tree.");
                        break;
                    }
                }else {
                    System.out.println(key+" found in the binary tree.");
                    break;
                }
            }while (true);
        }
    }

    public static void main(String[] args) {

        /*Prepare the binary tree*/
        System.out.println("Prepare the binary tree:");
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

        /*Inorder print the current binary tree with 16 nodes*/
        System.out.println("Inorder print the current binary tree with 16 nodes:");
        tree.inorderTreePrint(tree.ROOT);
        System.out.println();

        /*Search Node 765 in current binary tree*/
        System.out.println("Search Node 765 in current binary tree:");
        searchAndInsertNode(765);
    }
}
```

---
#Outputs
```
Prepare the binary tree:
 1: 503: not found in the current tree, and then insert it in the tree.
 2:  87: not found in the current tree, and then insert it in the tree.
 3: 512: not found in the current tree, and then insert it in the tree.
 4:  61: not found in the current tree, and then insert it in the tree.
 5: 908: not found in the current tree, and then insert it in the tree.
 6: 170: not found in the current tree, and then insert it in the tree.
 7: 897: not found in the current tree, and then insert it in the tree.
 8: 275: not found in the current tree, and then insert it in the tree.
 9: 653: not found in the current tree, and then insert it in the tree.
10: 426: not found in the current tree, and then insert it in the tree.
11: 154: not found in the current tree, and then insert it in the tree.
12: 509: not found in the current tree, and then insert it in the tree.
13: 612: not found in the current tree, and then insert it in the tree.
14: 677: not found in the current tree, and then insert it in the tree.
15: 765: not found in the current tree, and then insert it in the tree.
16: 703: not found in the current tree, and then insert it in the tree.

Inorder print the current binary tree with 16 nodes:
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

Search Node 765 in current binary tree:
765 found in the binary tree.
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
