# java-NC211 旋转链表


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
     * NC211 旋转链表
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param head ListNode类
         * @param k int整型
         * @return ListNode类
         */
        public ListNode rotateLinkedList (ListNode head, int k) {
            return solution1(head, k);
            // return solution2(head, k);
        }
    
        /**
         * 指针
         * @param head
         * @param k
         * @return
         */
        private ListNode solution1(ListNode head, int k){
            if(head == null){
                return null;
            }
            // 统计节点数
            int n = 1;
            ListNode tail = head;
            while(tail.next != null){
                n++;
                tail = tail.next;
            }
    
            k = k%n;
            if(k == 0){
                return head;
            }
            
            int cnt = n-k;
            ListNode dummyHead = head;
            while(--cnt > 0){
                dummyHead = dummyHead.next;
            }
            
            ListNode pre = dummyHead;
            dummyHead = dummyHead.next;
            pre.next = null;
            tail.next = head;
    
            return dummyHead;
        }
    
        /**
         * 双指针: 快慢指针
         * @param head
         * @param k
         * @return
         */
        private ListNode solution2(ListNode head, int k){
            if(head == null){
                return null;
            }
            // 统计节点数
            int n = 1;
            ListNode tail = head;
            while(tail.next != null){
                n++;
                tail = tail.next;
            }
    
            k = k%n;
            if(k == 0){
                return head;
            }
    
            ListNode fast = head;
            int step = k;
            while(step-- > 0){
                fast = fast.next;
            }
    
            ListNode slow = head;
            while(fast.next != null){
                fast = fast.next;
                slow = slow.next;
            }
    
            fast.next = head;
            head = slow.next;
            slow.next = null;
    
            return head;
        }
    }

  

