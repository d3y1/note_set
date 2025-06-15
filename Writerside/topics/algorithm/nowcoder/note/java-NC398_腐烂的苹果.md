# java-NC398 腐烂的苹果


    import java.util.*;
    
    /**
     * NC398 腐烂的苹果
     * @author d3y1
     */
    public class Solution {
        private int ROW;
        private int COL;
        private int[] dx = new int[]{0, 1, 0, -1};
        private int[] dy = new int[]{1, 0, -1, 0};
        private int result = -1;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * @param grid int整型ArrayList<ArrayList<>>
         * @return int整型
         */
        public int rotApple (ArrayList<ArrayList<Integer>> grid) {
            ROW = grid.size();
            COL = grid.get(0).size();
    
            bfs(grid);
    
            // bfs遍历后 检查是否仍然有完好的苹果
            for(int i=0; i<ROW; i++){
                for(int j=0; j<COL; j++){
                    if(grid.get(i).get(j) == 1){
                        return -1;
                    }
                }
            }
    
            return result;
        }
    
        /**
         * bfs
         * @param grid
         */
        private void bfs(ArrayList<ArrayList<Integer>> grid){
            Queue<Step> queue = new LinkedList<>();
    
            for(int i=0; i<ROW; i++){
                for(int j=0; j<COL; j++){
                    // rotten apples at the beginning
                    if(grid.get(i).get(j) == 2){
                        queue.offer(new Step(i, j));
                    }
                }
            }
    
            int size;
            int level = -1;
            Step curr;
            int nextX,nextY;
            while(!queue.isEmpty()){
                size = queue.size();
                level++;
                while(size-- > 0){
                    curr = queue.poll();
                    for(int i=0; i<4; i++){
                        nextX = curr.x + dx[i];
                        nextY = curr.y + dy[i];
                        if(isValid(nextX, nextY)){
                            if(grid.get(nextX).get(nextY) == 1){
                                grid.get(nextX).set(nextY, 2);
                                queue.offer(new Step(nextX, nextY));
                            }
                        }
                    }
                }
            }
    
            result = level;
        }
    
        /**
         * 是否合法(是否越界)
         * @param x
         * @param y
         * @return
         */
        private boolean isValid(int x, int y){
            if(x<0 || x>=ROW || y<0 || y>=COL){
                return false;
            }
    
            return true;
        }
    
        /**
         * 苹果坐标
         */
        private class Step {
            int x;
            int y;
    
            public Step(int x, int y){
                this.x = x;
                this.y = y;
            }
        }
    }

  

