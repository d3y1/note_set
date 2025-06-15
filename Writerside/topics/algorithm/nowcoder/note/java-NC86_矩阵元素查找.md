# java-NC86 矩阵元素查找


    import java.util.*;
    
    /**
     * NC86 矩阵元素查找
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param mat int整型二维数组 
         * @param n int整型 
         * @param m int整型 
         * @param x int整型 
         * @return int整型一维数组
         */
        public int[] findElement (int[][] mat, int n, int m, int x) {
            // return solution1(mat, n, m, x);
            return solution2(mat, n, m, x);
        }
    
        /**
         * 二分: 每行
         * @param mat
         * @param n
         * @param m
         * @param x
         * @return
         */
        private int[] solution1(int[][] mat, int n, int m, int x){
            int left;
            int right;
            int mid;
            // 每行
            for(int row=0; row<n; row++){
                if(x<mat[row][0] || mat[row][m-1]<x){
                    continue;
                }
                // 二分
                left = 0;
                right = m-1;
                while(left <= right){
                    mid = (left+right)/2;
                    if(mat[row][mid] < x){
                        left = mid + 1;
                    }else if(mat[row][mid] > x){
                        right = mid -1;
                    }else{
                        return new int[]{row, mid};
                    }
                }
            }
    
            return new int[2];
        }
    
        /**
         * 二分: 每步向上或向右(从左下至右上)
         * @param mat
         * @param n
         * @param m
         * @param x
         * @return
         */
        private int[] solution2(int[][] mat, int n, int m, int x){
            // 每步向上或向右(从左下至右上)
            for(int row=n-1,col=0; row>=0&&col<m;){
                // 向右
                if(mat[row][col] < x){
                    col++;
                }
                // 向上
                else if(mat[row][col] > x){
                    row--;
                }
                // 相等
                else{
                    return new int[]{row,col};
                }
            }
    
            return new int[2];
        }
    }

  

