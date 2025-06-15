# java - HJ35 蛇形矩阵


    import java.util.Scanner;
    
    // 00 | 10 01 | 20 11 02 | 30 21 12 03 | ...
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            int num = in.nextInt();
            int[][] array = new int[num][num];
    
            int start = 1;
            for(int i=0; i<num; i++){
                for(int j=i, k=0; j>=0; j--,k++){
                    array[j][k] = start++;
                }
            }
    
            for(int i=0; i<num; i++){
                for(int j=0; j<num-i; j++){
                    System.out.print(array[i][j]+" ");
                }
                System.out.println();
            }
        }
    }

  

