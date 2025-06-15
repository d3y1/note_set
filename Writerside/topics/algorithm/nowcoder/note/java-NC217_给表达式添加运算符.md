# java-NC217 给表达式添加运算符


    import java.util.*;
    
    /**
     * NC217 给表达式添加运算符
     * @author d3y1
     */
    public class Solution {
        private List<String> resultList = new ArrayList<>();
        private char[] op = new char[]{'+', '-', '*'};
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param num string字符串
         * @param target int整型
         * @return string字符串一维数组
         */
        public String[] addOpt (String num, int target) {
            dfs1(num, target, 0, "", 0, 0);
            // dfs2(num, target, 0, "");
    
            String[] resArray = new String[resultList.size()];
            for(int i=0; i<resultList.size(); i++){
                resArray[i] = resultList.get(i);
            }
            return resArray;
        }
    
        /**
         * dfs
         * @param num
         * @param target
         * @param index
         * @param opStr
         * @param result
         * @param last
         */
        private void dfs1(String num, int target, int index, String opStr, int result, int last){
            if(index == num.length()){
                if(result == target){
                    resultList.add(opStr);
                }
                return;
            }
    
            int curr;
            if(index == 0){
                curr = num.charAt(index)-'0';
                dfs1(num, target, index+1, opStr+num.charAt(index)+"+", result+last+curr, curr);
            }else{
                curr = num.charAt(index)-'0';
                // +
                dfs1(num, target, index+1, opStr+num.charAt(index)+"+", result+last+curr, curr);
                // -
                dfs1(num, target, index+1, opStr+num.charAt(index)+"-", result+last-curr, curr);
                // * 需要回退补值(result-last+last*curr)
                dfs1(num, target, index+1, opStr+num.charAt(index)+"*", result-last+last*curr, curr);
            }
        }
    
        /**
         * dfs
         * @param num
         * @param target
         * @param index
         * @param opStr
         */
        private void dfs2(String num, int target, int index, String opStr){
            if(index == num.length()-1){
                opStr += num.charAt(index);
                if(isTarget(opStr, target)){
                    resultList.add(opStr);
                }
                return;
            }
    
            for(int i=0; i<3; i++){
                dfs2(num, target, index+1, opStr+num.charAt(index)+op[i]);
            }
        }
    
        /**
         * 是否目标值
         * @param opStr
         * @param target
         * @return
         */
        private boolean isTarget(String opStr, int target){
            Stack<String> stack = new Stack<>();
            int curr,last;
            for(char ch: opStr.toCharArray()){
                if(!stack.isEmpty() && stack.peek().equals("*")){
                    curr = ch-'0';
                    stack.pop();
                    last = Integer.parseInt(stack.pop());
                    stack.push(String.valueOf(last*curr));
                }else{
                    stack.push(String.valueOf(ch));
                }
            }
    
            int result = 0;
            String op;
            while(!stack.isEmpty()){
                curr = Integer.parseInt(stack.pop());
                if(!stack.isEmpty()){
                    op = stack.pop();
                    if(op.equals("+")){
                        if(!stack.isEmpty()){
                            last = Integer.parseInt(stack.pop());
                            result = last+curr;
                            stack.push(String.valueOf(result));
                        }
                    }else if(op.equals("-")){
                        if(!stack.isEmpty()){
                            last = Integer.parseInt(stack.pop());
                            result = last-curr;
                            stack.push(String.valueOf(result));
                        }
                    }
                }else{
                    result = curr;
                }
            }
    
            return result==target;
        }
    }

  

