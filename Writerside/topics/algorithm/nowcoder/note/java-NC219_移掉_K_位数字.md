# java-NC219 移掉 K 位数字


    import java.util.*;
    
    /**
     * NC219 移掉 K 位数字
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param num string字符串
         * @param k int整型
         * @return string字符串
         */
        public String removeKnums (String num, int k) {
            // return solution1(num, k);
            // return solution2(num, k);
            return solution3(num, k);
        }
    
        /**
         * 单调栈+贪心
         * @param num
         * @param k
         * @return
         */
        private String solution1(String num, int k){
            if(k >= num.length()){
                return "0";
            }
    
            Stack<Character> stack = new Stack<>();
            for(char digit: num.toCharArray()){
                // 单调栈(单调增)
                while(!stack.isEmpty() && digit<stack.peek() && k>0){
                    // 贪心
                    stack.pop();
                    k--;
                }
                stack.push(digit);
            }
    
            // 继续移除
            while(k-- > 0){
                if(!stack.isEmpty()){
                    stack.pop();
                }
            }
    
            // 保存结果
            StringBuilder sb = new StringBuilder();
            while(!stack.isEmpty()){
                sb.insert(0, stack.pop());
            }
    
            // 去掉前导0
            String result = sb.toString();
            if(result.startsWith("0")){
                int index;
                for(index=0; index<result.length(); index++){
                    if(result.charAt(index) != '0'){
                        break;
                    }
                }
                if(index < result.length()){
                    result = result.substring(index);
                }else{
                    result = "0";
                }
            }
    
            return result;
        }
    
        /**
         * 单调栈+贪心
         * @param num
         * @param k
         * @return
         */
        private String solution2(String num, int k){
            int n = num.length();
            if(k >= n){
                return "0";
            }
    
            Deque<Character> stack = new ArrayDeque<>();
    
            for(char ch: num.toCharArray()){
                // 单调栈(单调增)
                while(!stack.isEmpty() && stack.peekLast()>ch && k>0){
                    // 贪心
                    stack.pollLast();
                    k--;
                }
                stack.offerLast(ch);
            }
    
            // 继续移除
            while(!stack.isEmpty() && k>0){
                stack.pollLast();
                k--;
            }
    
            // 去掉前导0
            while(!stack.isEmpty() && stack.peekFirst()=='0'){
                stack.pollFirst();
            }
    
            // 保存结果
            StringBuilder sb = new StringBuilder();
            while(!stack.isEmpty()){
                sb.append(stack.pollFirst());
            }
    
            return sb.length()==0?"0":sb.toString();
        }
    
        /**
         * 单调栈+贪心
         * @param num
         * @param k
         * @return
         */
        private String solution3(String num, int k){
            int n = num.length();
            if(k >= n){
                return "0";
            }
    
            Deque<Character> stack = new ArrayDeque<>();
    
            for(char ch: num.toCharArray()){
                // 单调栈(单调增)
                while(!stack.isEmpty() && stack.peekLast()>ch && k>0){
                    // 贪心
                    stack.pollLast();
                    k--;
                }
                stack.offerLast(ch);
            }
    
            // 继续移除
            while(!stack.isEmpty() && k>0){
                stack.pollLast();
                k--;
            }
    
            // 保存结果
            StringBuilder sb = new StringBuilder();
            while(!stack.isEmpty()){
                sb.append(stack.pollFirst());
            }
    
            // 去掉前导0
            String result = sb.toString().replaceFirst("^0+", "");
    
            return "".equals(result)?"0":result;
        }
    }

  

