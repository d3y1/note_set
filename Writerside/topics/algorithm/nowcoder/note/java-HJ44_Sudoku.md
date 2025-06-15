# java-HJ44 Sudoku


    import java.util.Scanner;
    
    public class Main {
        private static final int NUM = 9;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 回溯法
         * @param in
         */
        private static void solution(Scanner in){
            int[][] matrix = new int[NUM+1][NUM+1];
    
            for(int i=1; i<=NUM; i++){
                for(int j=1; j<=NUM; j++){
                    matrix[i][j] = in.nextInt();
                }
            }
    
            trySudoku(matrix);
    
            for(int i=1; i<=NUM; i++){
                for(int j=1; j<=NUM; j++){
                    System.out.print(matrix[i][j]+" ");
                }
                System.out.println();
            }
        }
    
        /**
         * 递归
         * @param matrix
         * @return
         */
        private static boolean trySudoku(int[][] matrix){
            for(int i=1; i<=NUM; i++){
                for(int j=1; j<=NUM; j++){
                    if(matrix[i][j] != 0){
                        continue;
                    }
    
                    for(int val=1; val<=NUM; val++){
                        if(isValid(i, j, val, matrix)){
                            matrix[i][j] = val;
    
                            if(trySudoku(matrix)){
                                return true;
                            }
    
                            matrix[i][j] = 0;
                        }
                    }
                    return false;
                }
            }
            return true;
        }
    
        /**
         * 当前数字是否合法
         * @param row
         * @param col
         * @param val
         * @param matrix
         * @return
         */
        private static boolean isValid(int row, int col, int val, int[][] matrix){
            // 行
            for(int j=1; j<=NUM; j++){
                if(matrix[row][j] == val){
                    return false;
                }
            }
    
            // 列
            for(int i=1; i<=NUM; i++){
                if(matrix[i][col] == val){
                    return false;
                }
            }
    
            // 九宫格
            for(int i=((row-1)/3)*3+1; i<=((row-1)/3)*3+3; i++){
                for(int j=((col-1)/3)*3+1; j<=((col-1)/3)*3+3; j++){
                    if(matrix[i][j] == val){
                        return false;
                    }
                }
            }
    
            return true;
        }
    }

  

