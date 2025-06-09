# geohash编码
https://www.nowcoder.com/practice/46bd43f043c54013a67816d0a2946506

    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 二分法
         * @param in
         */
        private static void solution(Scanner in){
            int n = in.nextInt();
    
            int left = -90;
            int right = 90;
            int middle;
            int precision = 6;
            StringBuilder sb = new StringBuilder();
            while(precision-- > 0){
                middle = (left+right)/2;
                if(middle <= n){
                    sb.append(1);
                    left = middle;
                }else{
                    sb.append(0);
                    right = middle;
                }
            }
    
            System.out.println(sb);
        }
    }
    

