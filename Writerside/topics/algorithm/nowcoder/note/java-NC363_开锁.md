# java-NC363 开锁


    import java.util.*;
    
    /**
     * NC363 开锁
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param vec string字符串ArrayList
         * @param tar string字符串
         * @return int整型
         */
        public int open (ArrayList<String> vec, String tar) {
            // return solution1(vec, tar);
            return solution2(vec, tar);
        }
    
        // 禁止集合
        private HashSet<String> isForbidden;
        // 已访问集合
        private HashSet<String> isVisited = new HashSet<>();
        // 旋转: 上转 下转
        private final int[] rotate = new int[]{1, -1};
        // 开始密码
        private final String START = "0000";
        // 目标密码
        private String TARGET;
        // 最终结果
        private int result = -1;
        
        /**
         * bfs
         * @param vec
         * @param tar
         * @return
         */
        private int solution1(ArrayList<String> vec, String tar){
            isForbidden = new HashSet<>(vec);
            TARGET = tar;
    
            bfs();
    
            return result;
        }
    
        /**
         * bfs
         * 等价于 图的最短路径
         */
        private void bfs(){
            Queue<String> queue = new LinkedList<>();
            queue.offer(START);
            isVisited.add(START);
    
            String curr;
            HashSet<String> nextSet;
            int level = -1;
            int size;
            while(!queue.isEmpty()){
                size = queue.size();
                level++;
                while(size-- > 0){
                    curr = queue.poll();
                    if(curr.equals(TARGET)){
                        result = level;
                        return;
                    }
                    // nextSet = nextCodes(curr);
                    nextSet = nextCiphers(curr);
                    for(String code: nextSet){
                        queue.offer(code);
                        isVisited.add(code);
                    }
                }
            }
        }
    
        /**
         * 下一个密码
         * @param curr
         * @return
         */
        private HashSet<String> nextCodes(String curr){
            HashSet<String> nextSet = new HashSet<>();
            int digit,nextDigit;
            String code;
            for(int i = 0; i < 4; i++){
                digit = curr.charAt(i)-'0';
                for(int j = 0; j <= 1; j++){
                    nextDigit = (digit+rotate[j]+10)%10;
                    code = curr.substring(0, i) + nextDigit + curr.substring(i+1);
                    if(!isForbidden.contains(code) && !isVisited.contains(code)){
                        nextSet.add(code);
                    }
                }
            }
    
            return nextSet;
        }
    
        /**
         * 下一个密码
         * @param code
         * @return
         */
        private HashSet<String> nextCiphers(String code){
            HashSet<String> nextSet = new HashSet<>();
            String up,down;
            for(int i = 0; i < 4; i++){
                up = plusOne(code, i);
                if(!isForbidden.contains(up) && !isVisited.contains(up)){
                    nextSet.add(up);
                }
                down = minusOne(code, i);
                if(!isForbidden.contains(down) && !isVisited.contains(down)){
                    nextSet.add(down);
                }
            }
    
            return nextSet;
        }
    
        /**
         * 向上转一位
         * @param code
         * @param i
         * @return
         */
        private String plusOne(String code, int i){
            char[] chs = code.toCharArray();
            if(chs[i] == '9'){
                chs[i] = '0';
            }else{
                chs[i] += 1;
            }
    
            return new String(chs);
        }
    
        /**
         * 向下转一位
         * @param code
         * @param i
         * @return
         */
        private String minusOne(String code, int i){
            char[] chs = code.toCharArray();
            if(chs[i] == '0'){
                chs[i] = '9';
            }else{
                chs[i] -= 1;
            }
    
            return new String(chs);
        }
    
        //////////////////////////////////////////////////////////////////////////////////
    
        // 禁止集合
        private HashSet<String> forbid = new HashSet<>();
        // 已访问集合
        private HashSet<String> visited = new HashSet<>();
        // 旋转: 上转 下转
        private int[] turns = new int[]{-1, 1};
        // 开始密码
        private String start = "0000";
        // 目标密码
        private String target;
    
        /**
         * bfs
         * @param vec
         * @param tar
         * @return
         */
        private int solution2(ArrayList<String> vec, String tar){
            target = tar;
            for(String code: vec){
                forbid.add(code);
            }
    
            return bfs(start);
        }
    
        private int bfs(String start){
            int result = -1;
            Queue<String> queue = new LinkedList<>();
            queue.offer(start);
    
            int step = -1;
            int size;
            String code,next;
            char[] codeChs;
            char ch,nextCh;
            while(!queue.isEmpty()){
                size = queue.size();
                step++;
                while(size-- > 0){
                    code = queue.poll();
    
                    if(code.equals(target)){
                        return step;
                    }
                    for(int i=0; i<4; i++){
                        codeChs = code.toCharArray();
                        ch = codeChs[i];
                        for(int j=0; j<2; j++){
                            nextCh = (char) (((ch-'0'+turns[j]+10)%10)+'0');
                            codeChs[i] = nextCh;
                            next = String.valueOf(codeChs);
                            if(!forbid.contains(next)){
                                if(!visited.contains(next)){
                                    visited.add(next);
                                    queue.offer(next);
                                }
                            }
                        }
                    }
                }
            }
    
            return result;
        }
    }

  

