# java-NC24 删除有序链表中重复的元素-II


    import java.util.*;
    
    /*
     * public class ListNode {
     *   int val;
     *   ListNode next = null;
     *   public ListNode(int val) {
     *     this.val = val;
     *   }
     * }
     */
    
    /**
     * NC24 删除有序链表中重复的元素-II
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param head ListNode类
         * @return ListNode类
         */
        public ListNode deleteDuplicates (ListNode head) {
            return solution1(head);
            // return solution2(head);
        }
    
        /**
         * 链表
         * @param head
         * @return
         */
        private ListNode solution1(ListNode head){
            ListNode dummyHead = new ListNode(-1);
            dummyHead.next = head;
            ListNode pre = dummyHead;
            ListNode curr = pre.next;
            while(curr!=null && curr.next!=null){
                // 重复
                if(curr.val == curr.next.val){
                    curr = curr.next;
                    while(curr.next!=null && curr.val==curr.next.val){
                        curr = curr.next;
                    }
                    pre.next = curr.next;
                }
                // 不重复
                else{
                    pre = curr;
                }
                curr = curr.next;
            }
    
            return dummyHead.next;
        }
    
        /**
         * 链表
         * @param head
         * @return
         */
        private ListNode solution2(ListNode head){
            ListNode dummyHead = new ListNode(-1);
            dummyHead.next = head;
            ListNode curr = dummyHead;
            int val;
            while(curr.next!=null && curr.next.next!=null){
                // 重复
                if(curr.next.val == curr.next.next.val){
                    val = curr.next.val;
                    while(curr.next!=null && curr.next.val==val){
                        curr.next = curr.next.next;
                    }
                }
                // 不重复
                else{
                    curr = curr.next;
                }
            }
    
            return dummyHead.next;
        }
    }

  

