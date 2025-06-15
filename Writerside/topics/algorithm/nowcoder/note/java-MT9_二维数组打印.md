# java-MT9 二维数组打印


    import java.util.*;
    
    public class Printer {
        /**
         * 二维数组
         *
         * 举例子找规律
         * 
         *   0  1  2  3
         * 0 1  2  3  4
         * 1 5  6  7  8
         * 2 9  10 11 12
         * 3 13 14 15 16
         * 
         * 返回值 [4,3,8,2,7,12,1,6,11,16,5,10,15,9,14,13], 坐标依次如下:
         * 
         * 03
         * 02 13
         * 01 12 23
         * 00 11 22 33
         * 10 21 32
         * 20 31
         * 30
         *
         * @param arr
         * @param n
         * @return
         */
        public int[] arrayPrint(int[][] arr, int n) {
            int[] result = new int[n*n];
    
            int k = 0;
            for(int i=0,j=n-1; i<n&&j<n;){
                for(int p=i,q=j; p<n&&q<n; p++,q++){
                    result[k++] = arr[p][q];
                }
                if(j > 0){
                    j--;
                }else{
                    i++;
                }
            }
    
            return result;
        }
    }

  

