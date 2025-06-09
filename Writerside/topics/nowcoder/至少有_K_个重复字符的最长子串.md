# 至少有 K 个重复字符的最长子串
https://www.nowcoder.com/practice/5aabbcfc45e2443ab7b8c9988bca6616

    import java.util.*;
    
    /**
     * NC364 至少有 K 个重复字符的最长子串
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param s string字符串 
         * @param k int整型 
         * @return int整型
         */
        public int longestSubstring (String s, int k) {
            return solution1(s, k);
            // return solution2(s, k);
        }
    
        /**
         * 滑动窗口
         * @param s
         * @param k
         * @return
         */
        private int solution1(String s, int k){
            int len = s.length();
            if(k == 1){
                return len;
            }
            if(len < k){
                return 0;
            }
    
            // 可能的最大窗口
            int max = 0;
            int[] count = new int[26];
            for(char ch: s.toCharArray()){
                count[ch-'a']++;
            }
            for(int i=0; i<26; i++){
                if(count[i] >= k){
                    max += count[i];
                }
            }
    
            // 滑动窗口
            for(int gap=max; gap>=k; gap--){
                for(int i=0; i+gap<=len; i++){
                    if(isValid(s.substring(i, i+gap), k)){
                        return gap;
                    }
                }
            }
    
            return 0;
        }
    
        /**
         * 子串是否合法
         * @param sub
         * @param k
         * @return
         */
        private boolean isValid(String sub, int k){
            int[] count = new int[26];
            for(char ch: sub.toCharArray()){
                count[ch-'a']++;
            }
    
            for(int i=0; i<26; i++){
                if(0<count[i] && count[i]<k){
                    return false;
                }
            }
    
            return true;
        }
        
    
        /**
         * 分治法
         * @param s
         * @param k
         * @return
         */
        private int solution2(String s, int k){
            return divide(s, k);
        }
    
        /**
         * 递归: 分治
         * @param s
         * @param k
         * @return
         */
        private int divide(String s, int k){
            int len = s.length();
            if(k == 1){
                return len;
            }
            if(len < k){
                return 0;
            }
    
            HashMap<Character, Integer> map = new HashMap<>();
            for(char ch: s.toCharArray()){
                map.put(ch, map.getOrDefault(ch, 0)+1);
            }
    
            for(char ch: s.toCharArray()){
                if(map.get(ch) < k){
                    int maxLen = 0;
                    for(String part: s.split(String.valueOf(ch))){
                        maxLen = Math.max(maxLen, divide(part, k));
                    }
                    return maxLen;
                }
            }
    
            return s.length();
        }
    }
    

