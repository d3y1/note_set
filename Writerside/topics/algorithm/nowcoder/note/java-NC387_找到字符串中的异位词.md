# java-NC387 找到字符串中的异位词


    import java.util.*;
    
    /**
     * NC387 找到字符串中的异位词
     * @author d3y1
     */
    public class Solution {
        private String key;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC356 至多包含K种字符的子串 [nowcoder]
         *
         * @param s string字符串
         * @param p string字符串
         * @return int整型一维数组
         */
        public ArrayList<Integer> findWord (String s, String p) {
            // return solution1(s,p);
            return solution2(s,p);
        }
    
        /**
         * 双指针(滑动窗口)
         * @param s
         * @param p
         * @return
         */
        private ArrayList<Integer> solution1(String s, String p){
            int lenS = s.length();
            int lenP = p.length();
    
            key = sortWord(p);
    
            String sub;
            ArrayList<Integer> list = new ArrayList<>();
            // 双指针(滑动窗口)
            for(int i=0,j=i+lenP; j<=lenS; i++,j++){
                sub = s.substring(i,j);
                if(isAnagram(sub)){
                    list.add(i);
                }
            }
    
            return list;
        }
    
        /**
         * 是否异位词
         * @param sub
         * @return
         */
        private boolean isAnagram(String sub){
            sub = sortWord(sub);
            return sub.equals(key);
        }
    
        /**
         * 词排序
         * @param word
         * @return
         */
        private String sortWord(String word){
            char[] chs = word.toCharArray();
            Arrays.sort(chs);
            return String.valueOf(chs);
        }
    
        /**
         * 双指针
         * @param s
         * @param p
         * @return
         */
        private ArrayList<Integer> solution2(String s, String p){
            int lenS = s.length();
            int lenP = p.length();
    
            int[] cntS = new int[26];
            int[] cntP = new int[26];
            for(int i=0; i<lenP; i++){
                cntP[p.charAt(i)-'a']++;
            }
    
            char chL,chR;
            ArrayList<Integer> list = new ArrayList<>();
            // 双指针 毛毛虫
            for(int i=0,j=0; j<lenS; j++){
                chR = s.charAt(j);
                cntS[chR-'a']++;
                while(cntS[chR-'a'] > cntP[chR-'a']){
                    chL = s.charAt(i);
                    cntS[chL-'a']--;
                    i++;
                }
                if(j-i+1 == lenP){
                    list.add(i);
                }
            }
    
            return list;
        }
    }

  

