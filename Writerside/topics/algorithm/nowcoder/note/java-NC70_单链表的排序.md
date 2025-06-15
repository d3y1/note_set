# java-NC70 单链表的排序


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
     * NC70 单链表的排序
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param head ListNode类 the head node
         * @return ListNode类
         */
        public ListNode sortInList (ListNode head) {
            // return solution1(head);
            return solution2(head);
            // return solution3(head);
        }
    
        /**
         * 堆排序
         * @param head
         * @return
         */
        private ListNode solution1(ListNode head){
            // PriorityQueue<ListNode> minHeap = new PriorityQueue<>((o1, o2) -> (o1.val-o2.val));
            PriorityQueue<ListNode> minHeap = new PriorityQueue<>(Comparator.comparingInt(o -> o.val));
    
            while(head != null){
                minHeap.offer(new ListNode(head.val));
                head = head.next;
            }
    
            ListNode top;
            ListNode tail = new ListNode(-1);
            if(!minHeap.isEmpty()){
                top = minHeap.poll();
                head = top;
                tail = top;
            }
    
            while(!minHeap.isEmpty()){
                top = minHeap.poll();
                tail.next = top;
                tail = tail.next;
            }
    
            return head;
        }
    
        /**
         * 归并排序(自顶向下)
         * @param head
         * @return
         */
        private ListNode solution2(ListNode head){
            return mergeSort(head);
        }
    
        /**
         * 归并
         * @param head
         * @return
         */
        private ListNode mergeSort(ListNode head){
            if(head==null || head.next==null){
                return head;
            }
    
            ListNode dummyHead = new ListNode(-1);
            dummyHead.next = head;
            ListNode fast = dummyHead;
            ListNode slow = dummyHead;
            while(fast!=null && fast.next!=null){
                fast = fast.next.next;
                slow = slow.next;
            }
    
            ListNode left = head;
            ListNode right = slow.next;
            slow.next = null;
    
            return merge(mergeSort(left), mergeSort(right));
        }
    
        /**
         * 合并
         * @param left
         * @param right
         * @return
         */
        private ListNode merge(ListNode left, ListNode right){
            ListNode tail = new ListNode(-1);
            ListNode head = tail;
    
            while(left!=null && right!=null){
                if(left.val <= right.val){
                    tail.next = left;
                    left = left.next;
                }else{
                    tail.next = right;
                    right = right.next;
                }
                tail = tail.next;
            }
    
            tail.next = (left!=null) ? left : right;
    
            return head.next;
        }
    
        /**
         * 归并排序(自底向上)
         * @param head
         * @return
         */
        public ListNode solution3(ListNode head) {
            if(head == null){
                return head;
            }
            
            int len = 0;
            ListNode node = head;
            while(node != null){
                len++;
                node = node.next;
            }
            
            ListNode dummyHead = new ListNode(-1);
            dummyHead.next = head;
            for(int subLen=1; subLen<len; subLen<<=1){
                ListNode prev = dummyHead;
                ListNode curr = dummyHead.next;
                while(curr != null){
                    ListNode left = curr;
                    for(int i=1; i<subLen&&curr.next!=null; i++){
                        curr = curr.next;
                    }
                    
                    ListNode right = curr.next;
                    curr.next = null;
                    curr = right;
                    for(int i=1; i<subLen&&curr!=null&&curr.next!=null; i++){
                        curr = curr.next;
                    }
                    
                    ListNode next = null;
                    if(curr != null){
                        next = curr.next;
                        curr.next = null;
                    }
                    
                    ListNode merged = merge(left, right);
                    prev.next = merged;
                    while(prev.next != null){
                        prev = prev.next;
                    }
                    curr = next;
                }
            }
            
            return dummyHead.next;
        }
    }

  

