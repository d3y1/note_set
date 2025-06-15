# java-HJ69 矩阵乘法


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
        
        private static void solution(Scanner in){
            int x = in.nextInt();
            int y = in.nextInt();
            int z = in.nextInt();
    
            int[][] matrixA = new int[x][y];
            int[][] matrixB = new int[y][z];
            int[][] matrixC = new int[x][z];
    
            // matrixA init
            for(int i=0; i<x; i++){
                for(int j=0; j<y; j++){
                    matrixA[i][j] = in.nextInt();
                }
            }
    
            // matrixB init
            for(int i=0; i<y; i++){
                for(int j=0; j<z; j++){
                    matrixB[i][j] = in.nextInt();
                }
            }
    
            // C = A X B
            for(int i=0; i<x; i++){
                for(int j=0; j<z; j++){
                    for(int k=0; k<y; k++){
                        matrixC[i][j] += matrixA[i][k] * matrixB[k][j];
                    }
                }
            }
    
            // print
            for(int i=0; i<x; i++){
                for(int j=0; j<z; j++){
                    System.out.print(matrixC[i][j]+" ");
                }
                System.out.println();
            }
        }
    }

  

