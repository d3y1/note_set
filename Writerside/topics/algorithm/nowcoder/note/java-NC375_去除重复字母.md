# java-NC375 去除重复字母


    import java.util.*;
    
    /**
     * NC375 去除重复字母
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param str string字符串
         * @return string字符串
         */
        public String removeDuplicateLetters (String str) {
            // return solution1(str);
            // return solution2(str);
            return solution3(str);
        }
    
        /**
         * 贪心+单调栈
         * @param str
         * @return
         */
        private String solution2(String str){
            int n = str.length();
    
            HashMap<Character, Integer> lastIndexMap = new HashMap<>();
            char cur;
            for(int i=n-1; i>=0; i--){
                cur = str.charAt(i);
                if(!lastIndexMap.containsKey(cur)){
                    lastIndexMap.put(cur, i);
                }
            }
    
            Deque<Integer> deque = new LinkedList<>();
            HashSet<Character> usedSet = new HashSet<>();
            // 贪心
            for(int i=0; i<n; i++){
                cur = str.charAt(i);
                // 测试用例: ambcadcb -> ambcd
                // 测试用例: mabcadcb -> mabcd
                if(usedSet.contains(cur)){
                    continue;
                }
                // 单调栈(单调增)
                // lastIndexMap.get(str.charAt(deque.peekLast()))>i -> 表示栈顶字符在右侧(后面)有重复
                while(!deque.isEmpty() && str.charAt(deque.peekLast())>cur && lastIndexMap.get(str.charAt(deque.peekLast()))>i){
                    usedSet.remove(str.charAt(deque.pollLast()));
                }
                deque.offerLast(i);
                usedSet.add(cur);
            }
    
            StringBuilder result = new StringBuilder();
            while(!deque.isEmpty()){
                result.append(str.charAt(deque.pollFirst()));
            }
    
            return result.toString();
        }
    
        /**
         * 贪心+单调栈
         * @param str
         * @return
         */
        private String solution3(String str){
            int n = str.length();
            char[] letters = str.toCharArray();
            int[] lastIndex = new int[26];
    
            // 当前字符 最后索引位置
            for(int i=0; i<n; i++){
                lastIndex[letters[i]-'a'] = i;
            }
    
            boolean[] isUsed = new boolean[26];
            Deque<Character> deque = new ArrayDeque<>();
            char cur;
            // 贪心
            for(int i=0; i<n; i++){
                cur = letters[i];
                if(isUsed[cur-'a']){
                    continue;
                }
                // 单调栈(单调增)
                // lastIndex[deque.peekLast()-'a']>i -> 表示栈顶字符在右侧(后面)有重复
                while(!deque.isEmpty() && deque.peekLast()>cur && lastIndex[deque.peekLast()-'a']>i){
                    isUsed[deque.pollLast()-'a'] = false;
                }
                deque.offerLast(cur);
                isUsed[cur-'a'] = true;
            }
    
            StringBuilder result = new StringBuilder();
            while(!deque.isEmpty()){
                result.append(deque.pollFirst());
            }
    
            return result.toString();
        }
    
        //////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 贪心+单调栈
         * @param str
         * @return
         */
        private String solution1(String str){
            Stack<Character> stack = new Stack<>();
            boolean[] isVisited = new boolean[26];
            int[] lastIndex = new int[26];
            char[] chars = str.toCharArray();
            int len = chars.length;
    
            for(int i=0; i<len; i++){
                lastIndex[chars[i]-'a'] = i;
            }
    
            // 贪心
            for(int i=0; i<len; i++){
                if(isVisited[chars[i]-'a']){
                    continue;
                }
                // 单调栈(单调增)
                // lastIndex[stack.peek()-'a']>i -> 表示栈顶字符在右侧(后面)有重复
                while(!stack.isEmpty() && stack.peek()>chars[i] && lastIndex[stack.peek()-'a']>i){
                    isVisited[stack.pop()-'a'] = false;
                }
                stack.push(chars[i]);
                isVisited[chars[i]-'a'] = true;
            }
    
            StringBuilder sb = new StringBuilder();
            while(!stack.isEmpty()){
                sb.append(stack.pop());
            }
    
            return sb.reverse().toString();
        }
    }

  

