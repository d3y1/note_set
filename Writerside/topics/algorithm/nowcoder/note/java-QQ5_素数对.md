# java-QQ5 素数对


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 数学法
         * @param in
         */
        private static void solution(Scanner in){
            int n = in.nextInt();
    
            int count = 0;
            for(int num=2,remain=n-num; num<=remain; num++,remain--){
                // 素数对
                if(isPrime(num) && isPrime(remain)){
                    count++;
                }
            }
    
            System.out.println(count);
        }
    
        /**
         * 是否素数
         * @param num
         * @return
         */
        private static boolean isPrime(int num){
            if(num <= 1){
                return false;
            }
            if(num == 2){
                return true;
            }
    
            for(int i=2; i<=Math.sqrt(num); i++){
                if(num%i == 0){
                    return false;
                }
            }
    
            return true;
        }
    }

  

