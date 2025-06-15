# java-NC356 至多包含K种字符的子串


    import java.util.*;
    
    /**
     * NC356 至多包含K种字符的子串
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param s string字符串
         * @param k int整型
         * @return int整型
         */
        public int longestSubstring (String s, int k) {
            // return solution1(s,k);
            return solution2(s,k);
        }
    
        /**
         * 双指针+哈希
         * @param s
         * @param k
         * @return
         */
        private int solution1(String s, int k){
            int n = s.length();
            if(n <= k){
                return n;
            }
    
            // 哈希
            HashMap<Character, Integer> map = new HashMap<>();
    
            int result = 0;
            char chL,chR;
            // 双指针 毛毛虫
            for(int i=0,j=0; j<n; j++){
                chR = s.charAt(j);
                map.put(chR, map.getOrDefault(chR, 0)+1);
                while(map.size() > k){
                    chL = s.charAt(i);
                    map.put(chL, map.get(chL)-1);
                    if(map.get(chL) == 0){
                        map.remove(chL);
                    }
                    i++;
                }
                result = Math.max(result, j-i+1);
            }
    
            return result;
        }
    
        /**
         * 双指针+哈希
         * @param s
         * @param k
         * @return
         */
        private int solution2(String s, int k){
            int n = s.length();
            if(n <= k){
                return n;
            }
    
            // 哈希
            int[] cnt = new int[26];
    
            int result = 0;
            int kind = 0;
            char chL,chR;
            char[] chars = s.toCharArray();
            // 双指针 毛毛虫
            for(int i=0,j=0; j<n; j++){
                chR = chars[j];
                cnt[chR-'a']++;
                // 从0到1 字符种类加1
                if(cnt[chR-'a'] == 1){
                    kind++;
                }
                while(kind > k){
                    chL = chars[i];
                    cnt[chL-'a']--;
                    // 从1到0 字符种类减1
                    if(cnt[chL-'a'] == 0){
                        kind--;
                    }
                    i++;
                }
                result = Math.max(result, j-i+1);
            }
    
            return result;
        }
    }

  

