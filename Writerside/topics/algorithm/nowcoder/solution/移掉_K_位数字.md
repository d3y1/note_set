# 移掉 K 位数字
https://www.nowcoder.com/practice/0fe685c8272d40f1b9785fedd2499c1c

    import java.util.*;
    
    /**
     * NC219 移掉 K 位数字
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 单调栈(单调增)
         *
         * @param num string字符串 
         * @param k int整型 
         * @return string字符串
         */
        public String removeKnums (String num, int k) {
            if(k >= num.length()){
                return "0";
            }
    
            // 单调栈(单调增)
            Stack<Character> stack = new Stack<>();
            for(char digit: num.toCharArray()){
                while(!stack.isEmpty() && digit<stack.peek() && k>0){
                    stack.pop();
                    k--;
                }
                stack.push(digit);
            }
    
            // 移除剩余次数
            while(k-- > 0){
                if(!stack.isEmpty()){
                    stack.pop();
                }
            }
    
            // 生成结果
            StringBuilder sb = new StringBuilder();
            while(!stack.isEmpty()){
                sb.insert(0, stack.pop());
            }
    
            // 去掉前导0
            String result = sb.toString();
            if(result.startsWith("0")){
                int index;
                for(index=0; index<result.length(); index++){
                    if(result.charAt(index) != '0'){
                        break;
                    }
                }
                if(index < result.length()){
                    result = result.substring(index);
                }else{
                    result = "0";
                }
            }
    
            return result;
        }
    }
    

