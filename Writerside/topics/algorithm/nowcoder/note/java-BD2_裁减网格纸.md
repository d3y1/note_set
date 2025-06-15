# java-BD2 裁减网格纸


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 贪心
         * @param in
         */
        private static void solution(Scanner in){
            int n = in.nextInt();
    
            int x,y;
            int minX = Integer.MAX_VALUE;
            int minY = Integer.MAX_VALUE;
            int maxX = Integer.MIN_VALUE;
            int maxY = Integer.MIN_VALUE;
            for(int i=1; i<=n; i++){
                x = in.nextInt();
                y = in.nextInt();
    
                minX = Math.min(minX, x);
                maxX = Math.max(maxX, x);
                minY = Math.min(minY, y);
                maxY = Math.max(maxY, y);
    
    //                if(x < minX){
    //                    minX = x;
    //                }
    //                if(x > maxX){
    //                    maxX = x;
    //                }
    //                if(y < minY){
    //                    minY = y;
    //                }
    //                if(y > maxY){
    //                    maxY = y;
    //                }
            }
    
            int edge = Math.max(maxX-minX, maxY-minY);
            System.out.println(edge*edge);
        }
    }

  

