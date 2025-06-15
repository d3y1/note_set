# java-NC260 复杂链表的复制


    import java.util.*;
    /*
    public class RandomListNode {
        int label;
        RandomListNode next = null;
        RandomListNode random = null;
    
        RandomListNode(int label) {
            this.label = label;
        }
    }
    */
    
    /**
     * NC260 复杂链表的复制
     * @author d3y1
     */
    public class Solution {
        public RandomListNode Clone(RandomListNode pHead) {
            // return solution1(pHead);
            return solution2(pHead);
        }
    
        /**
         * 哈希法
         * @param pHead
         * @return
         */
        private RandomListNode solution1(RandomListNode pHead){
            if(pHead == null){
                return null;
            }
    
            RandomListNode dummyHead = new RandomListNode(-1);
            RandomListNode tail = dummyHead;
            RandomListNode curr = pHead;
            RandomListNode clone;
    
            HashMap<RandomListNode,RandomListNode> map = new HashMap<>();
    
            // 处理next指针(尾插法)
            while(curr != null){
                clone = new RandomListNode(curr.label);
                // 映射 当前节点->克隆节点
                map.put(curr, clone);
                tail.next = clone;
                tail = tail.next;
                curr = curr.next;
            }
    
            // 处理random指针
            curr = pHead;
            while(curr != null){
                clone = map.get(curr);
                if(curr.random != null){
                    clone.random = map.get(curr.random);
                }
                curr = curr.next;
            }
    
            return dummyHead.next;
        }
    
        /**
         * 拷贝法
         * @param pHead
         * @return
         */
        private RandomListNode solution2(RandomListNode pHead){
            if(pHead == null){
                return null;
            }
    
            RandomListNode curr = pHead;
            RandomListNode clone;
    
            // 原地拷贝 连成一串
            while(curr != null){
                clone = new RandomListNode(curr.label);
                clone.next = curr.next;
                curr.next = clone;
                curr = clone.next;
            }
    
            // 处理random指针
            curr = pHead;
            while(curr != null){
                clone = curr.next;
                if(curr.random != null){
                    clone.random = curr.random.next;
                }
                curr = clone.next;
            }
    
            RandomListNode dummyHead = new RandomListNode(-1);
            dummyHead.next = pHead.next;
    
            // 处理next指针
            curr = pHead;
            while(curr != null){
                clone = curr.next;
                curr.next = clone.next;
                if(curr.next != null){
                    clone.next = curr.next.next;
                }
                curr = curr.next;
            }
    
            return dummyHead.next;
        }
    }
    

  

