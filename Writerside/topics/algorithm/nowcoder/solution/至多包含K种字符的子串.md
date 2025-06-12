# 至多包含K种字符的子串
https://www.nowcoder.com/practice/04c926ef687340c3842a72edb5c23ede

    import java.util.*;
    
    /**
     * NC356 至多包含K种字符的子串
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
            HashMap<Character, Integer> map = new HashMap<>();
            int len = s.length();
            int result = 0;
            // 双指针
            for(int i=0,j=0; j<len; j++){
                map.put(s.charAt(j), map.getOrDefault(s.charAt(j), 0)+1);
                int count;
                while(map.size() > k){
                    count = map.get(s.charAt(i));
                    if(count == 1){
                        map.remove(s.charAt(i));
                    }else{
                        map.put(s.charAt(i), count-1);
                    }
                    i++;
                }
                result = Math.max(result, j-i+1);
            }
    
            return result;
        }
    }
    

