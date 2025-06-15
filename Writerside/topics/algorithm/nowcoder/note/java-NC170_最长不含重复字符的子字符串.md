# java-NC170 最长不含重复字符的子字符串


    import java.util.*;
    
    /**
     * NC170 最长不含重复字符的子字符串
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC41 最长无重复子数组 [nowcoder]
         * 
         * @param s string字符串 
         * @return int整型
         */
        public int lengthOfLongestSubstring (String s) {
            // return solution1(s);
            // return solution2(s);
            // return solution3(s);
            // return solution4(s);
            return solution44(s);
            // return solution5(s);
            // return solution6(s);
            // return solution7(s);
        }
    
        /**
         * 双指针
         * @param s
         * @return
         */
        private int solution1(String s){
            int len = s.length();
            if(len == 0){
                return 0;
            }
    
            int result = 0;
            HashSet<Character> set = new HashSet<>();
            char chL,chR;
            for(int i=0,j=0; i<=j&&j<len; j++){
                chR = s.charAt(j);
                if(!set.contains(chR)){
                    result = Math.max(result, j-i+1);
                }else{
                    while(set.contains(chR)){
                        chL = s.charAt(i++);
                        set.remove(chL);
                    }
                }
                set.add(chR);
            }
    
            return result;
        }
    
        /**
         * HashMap
         * @param s
         * @return
         */
        private int solution2(String s){
            int left = -1, result = 0;
            HashMap<Character,Integer> map = new HashMap<>();
    
            for(int i = 0; i < s.length(); i++){
                if(map.containsKey(s.charAt(i))){
                    left = Math.max(left, map.get(s.charAt(i)));
                }
                map.put(s.charAt(i),i);
                result = Math.max(result, i-left);
            }
    
            return result;
        }
    
        /**
         * 动态规划
         *
         * dp[i]表示以下标i结尾的最长不含重复子串的长度
         *
         * @param s
         * @return
         */
        private int solution3(String s){
            int len = s.length();
            if(len == 0){
                return 0;
            }
    
            int[] dp = new int[len];
            int result = 1;
            HashMap<Character, Integer> map = new HashMap<>();
            dp[0] = 1;
            map.put(s.charAt(0), 0);
            for(int i=1; i<len; i++){
                dp[i] = 1;
                if(!map.containsKey(s.charAt(i))){
                    dp[i] = dp[i-1] + 1;
                }else{
                    dp[i] = Math.min(dp[i-1]+1, i-map.get(s.charAt(i)));
                }
                map.put(s.charAt(i),i);
    
                result = Math.max(result, dp[i]);
            }
    
            return result;
        }
    
        //////////////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 双指针+哈希(HashMap)
         * @param s
         * @return
         */
        private int solution4(String s){
            int n = s.length();
            // 哈希
            HashMap<Character,Integer> map = new HashMap<>();
            char key;
            int result = 0;
            // 双指针
            for(int i=0,j=0; j<n; j++){
                key = s.charAt(j);
                while(map.containsKey(key)){
                    map.remove(s.charAt(i++));
                }
                map.put(key, j);
                result = Math.max(result, j-i+1);
            }
    
            return result;
        }
    
        /**
         * 双指针+哈希(HashMap)
         * @param s
         * @return
         */
        private int solution44(String s){
            int n = s.length();
            // 哈希
            HashMap<Character,Integer> map = new HashMap<>();
            char key;
            int result = 0;
            // 双指针
            for(int i=0,j=0; j<n; j++){
                key = s.charAt(j);
                if(map.containsKey(key)){
                    i = Math.max(i, map.get(key)+1);
                }
                map.put(key, j);
                result = Math.max(result, j-i+1);
            }
    
            return result;
        }
    
        /**
         * 双指针+哈希(HashSet)
         * @param s
         * @return
         */
        private int solution5(String s){
            int n = s.length();
            // 哈希
            HashSet<Character> set = new HashSet<>();
            char key;
            int result = 0;
            // 双指针
            for(int i=0,j=0; j<n; j++){
                key = s.charAt(j);
                while(set.contains(key)){
                    set.remove(s.charAt(i++));
                }
                set.add(key);
                result = Math.max(result, j-i+1);
            }
    
            return result;
        }
    
        /**
         * 双指针+哈希(HashSet)
         * @param s
         * @return
         */
        private int solution6(String s){
            int n = s.length();
            // 哈希
            HashSet<Character> set = new HashSet<>();
            int result = 0;
            // 双指针
            int i=0,j=0;
            while(j < n){
                if(set.contains(s.charAt(j))){
                    set.remove(s.charAt(i));
                    i++;
                }else{
                    set.add(s.charAt(j));
                    j++;
                    result = Math.max(result, set.size());
                }
            }
    
            return result;
        }
    
        /**
         * 队列
         * @param s
         * @return
         */
        private int solution7(String s){
            int n = s.length();
            // 队列
            Queue<Character> queue = new LinkedList<>();
            int result = 0;
            int j=0;
            while(j < n){
                if(queue.contains(s.charAt(j))){
                    queue.poll();
                }else{
                    queue.offer(s.charAt(j));
                    j++;
                    result = Math.max(result, queue.size());
                }
            }
    
            return result;
        }
    }

  

