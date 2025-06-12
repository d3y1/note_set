# 设计LRU缓存结构
https://www.nowcoder.com/practice/5dfded165916435d9defb053c63f1e84

    import java.util.*;
    
    /**
     * NC93 设计LRU缓存结构
     * @author d3y1
     */
    public class Solution {
        private Deque<Integer> keyQueue = new LinkedList<>();
        private HashMap<Integer,Integer> kvMap = new HashMap<>();
        private int capacity;
    
        public Solution(int capacity) {
            this.capacity = capacity;
        }
    
        public int get(int key) {
            // 存在
            if(kvMap.containsKey(key)){
                keyQueue.remove(key);
                keyQueue.offerFirst(key);
                return kvMap.get(key);
            }
    
            // 不存在
            return -1;
        }
    
        public void set(int key, int value) {
            // 存在
            if(kvMap.containsKey(key)){
                keyQueue.remove(key);
            }
            // 不存在
            else{
                // LRU key
                int rmKey;
                if(keyQueue.size() >= capacity){
                    rmKey = keyQueue.peekLast();
                    kvMap.remove(rmKey);
                    keyQueue.remove(rmKey);
                }
            }
            keyQueue.offerFirst(key);
            kvMap.put(key, value);
        }
    }
    
    /**
     * Your Solution object will be instantiated and called as such:
     * Solution solution = new Solution(capacity);
     * int output = solution.get(key);
     * solution.set(key,value);
     */
    

