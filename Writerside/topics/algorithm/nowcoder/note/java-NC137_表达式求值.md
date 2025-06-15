# java-NC137 表达式求值


    import java.util.*;
    
    /**
     * NC137 表达式求值
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         * 
         * 相似 -> NC240 计算器(一)   [nowcoder]
         * 相似 -> NC241 计算器(二)   [nowcoder]
         * 相似 -> HJ50 四则运算      [nowcoder]
         *
         * 返回表达式的值
         * @param s string字符串 待计算的表达式
         * @return int整型
         */
        public int solve (String s) {
            int n = s.length();
            if(n == 0){
                return 0;
            }
    
            Stack<Integer> stack = new Stack<>();
    
            char sign = '+';
            int num;
            char ch;
            for(int i=0; i<n; i++){
                num = 0;
                ch = s.charAt(i);
    
                // 数字
                if(Character.isDigit(ch)){
                    num = num*10+(ch-'0');
                    while(++i < n){
                        ch = s.charAt(i);
                        if(Character.isDigit(ch)){
                            num = num*10+(ch-'0');
                        }else{
                            break;
                        }
                    }
                }
    
                // 括号 -> 递归
                if(ch == '('){
                    int cnt = 1;
                    int j;
                    for(j=i+1; j<n; j++){
                        ch = s.charAt(j);
                        if(ch == '('){
                            cnt++;
                        }
                        else if(ch == ')'){
                            cnt--;
                        }
                        if(cnt == 0){
                            num = solve(s.substring(i+1, j));
                            break;
                        }
                    }
                    i = j+1;
                }
    
                // 运算符
                switch(sign){
                    case '+': stack.push(num); break;
                    case '-': stack.push(-num); break;
                    case '*': stack.push(stack.pop()*num); break;
                    case '/': stack.push(stack.pop()/num); break;
                    default: break;
                }
    
                if(i == n){
                    break;
                }else{
                    sign = s.charAt(i);
                }
            }
    
            int result = 0;
            while(!stack.isEmpty()){
                result += stack.pop();
            }
    
            return result;
        }
    }

  

