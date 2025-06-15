# java-NC355 划分字母区间


    import java.util.*;
    
    /**
     * NC355 划分字母区间
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param s string字符串 
         * @return int整型ArrayList
         */
        public ArrayList<Integer> splitString (String s) {
            // return solution1(s);
            // return solution2(s);
            // return solution3(s);
            // return solution4(s);
            // return solution5(s);
            return solution55(s);
        }
    
        /**
         * 贪心+双指针+哈希
         * @param s
         * @return
         */
        private ArrayList<Integer> solution1(String s){
            HashMap<Character, Integer> rightMap = new HashMap<>();
            int n = s.length();
            for(int j=n-1; j>=0; j--){
                if(!rightMap.containsKey(s.charAt(j))){
                    rightMap.put(s.charAt(j), j);
                }
            }
    
            ArrayList<Integer> list = new ArrayList<>();
            // 双指针
            int left=0,right=0;
            char ch;
            for(int i=0; i<n; i++){
                ch = s.charAt(i);
                // 贪心 关键!
                right = Math.max(right, rightMap.get(ch));
                if(i == right){
                    list.add(right-left+1);
                    left = i+1;
                }
            }
    
            return list;
        }
    
        // /**
        //  * Double HashMap
        //  * @param s
        //  * @return
        //  */
        // private ArrayList<Integer> solution2(String s){
        //     HashMap<Character, Integer> leftMap = new HashMap<>();
        //     HashMap<Character, Integer> rightMap = new HashMap<>();
        //     int len =  s.length();
        //     for(int i=0,j=len-1; i<len&&j>=0; i++,j--){
        //         if(!leftMap.keySet().contains(s.charAt(i))){
        //             leftMap.put(s.charAt(i), i);
        //         }
        //         if(!rightMap.keySet().contains(s.charAt(j))){
        //             rightMap.put(s.charAt(j), j);
        //         }
        //     }
    
        //     ArrayList<Integer> list = new ArrayList<Integer>();
        //     int left,right;
        //     HashSet<Character> set = new HashSet<>();
        //     char ch;
        //     for(int i=0; i<len; ){
        //         ch = s.charAt(i);
        //         if(!set.contains(ch)){
        //             set.add(ch);
        //             left = leftMap.get(ch);
        //             right = rightMap.get(ch);
        //             if(left == right){
        //                 list.add(1);
        //             }else{
        //                 for(int j=left+1; j<right; j++){
        //                     ch = s.charAt(j);
        //                     if(!set.contains(ch)){
        //                         set.add(ch);
        //                         right = Math.max(right, rightMap.get(ch));
        //                     }
        //                 }
        //                 list.add(right-left+1);
        //             }
        //             i = right+1;
        //         }else{
        //             i++;
        //         }
        //     }
    
        //     return list;
        // }
    
        //////////////////////////////////////////////////////////////////////////
    
        /**
         * 贪心+双指针+字符串
         * @param s
         * @return
         */
        private ArrayList<Integer> solution3(String s){
            int n = s.length();
    
            ArrayList<Integer> result = new ArrayList<>();
            // 双指针
            int left = 0;
            int right = 0;
            int pre = -1;
            while(left < n){
                // 贪心 关键!
                right = Math.max(right, s.lastIndexOf(s.charAt(left)));
                if(left == right){
                    result.add(right-pre);
                    pre = right;
                }
                left++;
            }
    
            return result;
        }
    
        /**
         * 贪心+双指针+哈希
         * @param s
         * @return
         */
        private ArrayList<Integer> solution4(String s){
            int n = s.length();
    
            // 哈希 字符:最右索引
            HashMap<Character, Integer> rightIndexMap = new HashMap<>();
            char ch;
            for(int i=n-1; i>=0; i--){
                ch = s.charAt(i);
                if(!rightIndexMap.containsKey(ch)){
                    rightIndexMap.put(ch, i);
                }
            }
    
            ArrayList<Integer> result = new ArrayList<>();
            // 双指针
            int left = 0;
            int right = 0;
            for(int i=0; i<n; i++){
                ch = s.charAt(i);
                // 贪心 关键!
                right = Math.max(right, rightIndexMap.get(ch));
                if(i == right){
                    result.add(right-left+1);
                    left = i+1;
                }
            }
    
            return result;
        }
    
        /**
         * 贪心+双指针+哈希
         * @param s
         * @return
         */
        private ArrayList<Integer> solution5(String s){
            int n = s.length();
            // 哈希: 字符 -> 最右索引
            int[] rIdx = new int[26];
            for(int i=0; i<n; i++){
                rIdx[s.charAt(i)-'a'] = i;
            }
    
            ArrayList<Integer> result = new ArrayList<>();
            // 双指针
            int left = 0;
            int right = 0;
            for(int i=0; i<n; i++){
                // 贪心 关键!
                right = Math.max(right, rIdx[s.charAt(i)-'a']);
                if(i == right){
                    result.add(right-left+1);
                    left = i+1;
                }
            }
    
            return result;
        }
    
        /**
         * 贪心+双指针+哈希
         * @param s
         * @return
         */
        private ArrayList<Integer> solution55(String s){
            int n = s.length();
            char[] chars = s.toCharArray();
    
            // 哈希: 字符 -> 最右索引
            int[] rIdx = new int[26];
            for(int i=0; i<n; i++){
                rIdx[chars[i]-'a'] = i;
            }
    
            ArrayList<Integer> result = new ArrayList<>();
            // 双指针
            int left = 0;
            int right = 0;
            for(int i=0; i<n; i++){
                // 贪心 关键!
                right = Math.max(right, rIdx[chars[i]-'a']);
                if(i == right){
                    result.add(right-left+1);
                    left = i+1;
                }
            }
    
            return result;
        }
    }

  

