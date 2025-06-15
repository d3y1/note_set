# java-NC285 矩阵中的路径


    import java.util.*;
    
    /**
     * NC285 矩阵中的路径
     * @author d3y1
     */
    public class Solution {
        private int LEN;
        private boolean isFound = false;
        private int[] dx = new int[]{0, 1, 0, -1};
        private int[] dy = new int[]{1, 0, -1, 0};
        private boolean[][] isVisited;
        private int ROW;
        private int COL;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param matrix char字符型二维数组
         * @param word string字符串
         * @return bool布尔型
         */
        public boolean hasPath (char[][] matrix, String word) {
            LEN = word.length();
            ROW = matrix.length;
            COL = matrix[0].length;
            isVisited = new boolean[ROW][COL];
    
            for(int i = 0; i < ROW; i++){
                for(int j = 0; j < COL; j++){
                    if(matrix[i][j] == word.charAt(0)){
                        dfs(matrix, i, j, word, 0);
                    }
                }
            }
    
            return isFound;
        }
    
        /**
         * dfs
         * @param matrix
         * @param x
         * @param y
         * @param word
         * @param index
         */
        private void dfs(char[][] matrix, int x, int y, String word, int index){
            // 当前字符相同
            if(matrix[x][y] == word.charAt(index)){
                // 找到路径
                if(index+1 == LEN){
                    isFound = true;
                    return;
                }
                // 未找到路径
                if(!isFound){
                    // 下一步坐标
                    int nextX,nextY;
                    for(int i = 0; i < 4; i++){
                        nextX = x+dx[i];
                        nextY = y+dy[i];
                        // 合法
                        if(isValid(nextX, nextY)){
                            // 未访问过
                            if(!isVisited[nextX][nextY]){
                                // 标记已访问
                                isVisited[nextX][nextY] = true;
                                dfs(matrix, nextX, nextY, word, index+1);
                                // 标记未访问
                                isVisited[nextX][nextY] = false;
                            }
                        }
                    }
                }
            }
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
    }

  

