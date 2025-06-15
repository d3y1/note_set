# java-NC299 简化目录路径


    import java.util.*;
    
    /**
     * NC299 简化目录路径
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 栈(双端队列实现)
         *
         * @param path string字符串
         * @return string字符串
         */
        public String simplifyPath (String path) {
            Deque<String> stack = new ArrayDeque<>();
            String[] dirs = path.split("/");
    
            StringBuilder sb = new StringBuilder("");
    
            for(String dir: dirs){
                switch(dir){
                    // 空字符串
                    case "": break;
                    // 当前目录
                    case ".": break;
                    // 上级目录
                    case "..": if(!stack.isEmpty()){stack.pollLast();} break;
                    // 目录入栈
                    default: stack.offerLast(dir); break;
                }
            }
    
            // 简化目录
            if(stack.isEmpty()){
                return "/";
            }else{
                while(!stack.isEmpty()){
                    sb.append("/").append(stack.pollFirst());
                }
    
                return sb.toString();
            }
        }
    }

  

