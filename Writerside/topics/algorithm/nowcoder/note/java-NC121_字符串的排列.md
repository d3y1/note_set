# java-NC121 字符串的排列


    import java.util.*;
    
    /**
     * NC121 字符串的排列
     * @author d3y1
     */
    public class Solution {
        private HashSet<String> result = new HashSet<>();
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * @param str string字符串
         * @return string字符串ArrayList
         */
        public ArrayList<String> Permutation (String str) {
            dfs(str, 0);
    
            return new ArrayList<String>(result);
        }
    
        /**
         * dfs(递归)
         * @param str
         * @param curr
         */
        private void dfs(String str, int curr){
            result.add(str);
    
            char[] chars = str.toCharArray();
            for(int next=curr; next<str.length(); next++){
                swap(chars, curr, next);
                dfs(String.valueOf(chars), curr+1);
                swap(chars, curr, next);
            }
        }
    
        /**
         * 交换字符
         * @param chars
         * @param i
         * @param j
         */
        private void swap(char[] chars, int i, int j){
            char tmp = chars[i];
            chars[i] = chars[j];
            chars[j] = tmp;
        }
    }

  

