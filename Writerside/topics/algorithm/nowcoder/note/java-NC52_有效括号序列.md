# java-NC52 有效括号序列


    import java.util.*;
    
    /**
     * NC52 有效括号序列
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param s string字符串
         * @return bool布尔型
         */
        public boolean isValid (String s) {
            // 栈
            Stack<Character> stack = new Stack<>();
            for(char ch: s.toCharArray()){
                switch(ch){
                    case '(':
                    case '[':
                    case '{':
                        stack.push(ch);
                        break;
                    case ')':
                        if(stack.isEmpty() || stack.peek()!='('){
                            return false;
                        }
                        stack.pop();
                        break;
                    case ']':
                        if(stack.isEmpty() || stack.peek()!='['){
                            return false;
                        }
                        stack.pop();
                        break;
                    case '}':
                        if(stack.isEmpty() || stack.peek()!='{'){
                            return false;
                        }
                        stack.pop();
                        break;
                }
            }
    
            return stack.isEmpty();
        }
    }

  

