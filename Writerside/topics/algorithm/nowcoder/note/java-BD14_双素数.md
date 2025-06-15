# java-BD14 双素数


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法
         * @param in
         */
        private static void solution(Scanner in){
            int k = in.nextInt();
    
            StringBuilder sb;
            int positive,reverse;
            for(int i=2,count=0; count<k; i++){
                sb = new StringBuilder(String.valueOf(i));
                positive = i;
                reverse = Integer.parseInt(String.valueOf(sb.reverse()));
                if(positive != reverse){
                    // 双素数
                    if(isPrime(positive) && isPrime(reverse)){
                        count++;
                        if(count == k){
                            if(positive <= 1000000){
                                System.out.println(positive);
                            }else{
                                System.out.println(-1);
                            }
                            break;
                        }
                    }
                }
            }
        }
    
        /**
         * 是否素数
         * @param num
         * @return
         */
        private static boolean isPrime(int num){
            for(int i=2; i<=Math.sqrt(num); i++){
                if(num%i == 0){
                    return false;
                }
            }
    
            return true;
        }
    }

  

