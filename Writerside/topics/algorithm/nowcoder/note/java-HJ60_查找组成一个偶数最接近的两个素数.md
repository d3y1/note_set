# java-HJ60 查找组成一个偶数最接近的两个素数


    import java.util.HashSet;
    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
    
            Scanner in = new Scanner(System.in);
    
            while (in.hasNext()){
                solution(in.nextInt());
            }
        }
    
        // solution() optimize
        private static void solution(int even){
            for(int num=even/2; num<even; num++){
                if(isPrime(num) && isPrime(even-num)){
                    System.out.println(even-num);
                    System.out.println(num);
                    break;
                }
            }
        }
    
    //    private static void solution(int even){
    //        int min = -1;
    //        int max = -1;
    //        int interval = Integer.MAX_VALUE;
    //        for(int num=1; num<even; num++){
    //            if(isPrime(num) && isPrime(even-num)){
    //                if(Math.abs(even-2*num) < interval){
    //                    min = Math.min(num, even-num);
    //                    max = Math.max(num, even-num);
    //                    interval = Math.abs(even-2*num);
    //                }
    //            }
    //        }
    
    //        System.out.println(min);
    //        System.out.println(max);
    //    }
    
        private static boolean isPrime(int num){
            for(int i=2; i<=(int)(Math.sqrt(num)); i++){
                if(num%i == 0){
                    return false;
                }
            }
    
            return true;
        }
    
    //    public static void main(String[] args) {
    //
    //        Scanner in = new Scanner(System.in);
    //
    //        int even = in.nextInt();
    //
    //        HashSet<Integer> primeSet = new HashSet<>();
    //
    //        for(int num=1; num<even; num++){
    //            boolean isPrime = true;
    //            for(int j=(int)(Math.sqrt(num)); j>1; j--){
    //                if(num%j == 0){
    //                    isPrime = false;
    //                    break;
    //                }
    //            }
    //            if(isPrime){
    //                primeSet.add(num);
    //            }
    //        }
    //
    //        int min = -1;
    //        int max = -1;
    //        int interval = Integer.MAX_VALUE;
    //        for(Integer prime: primeSet) {
    //            if(primeSet.contains(even-prime)){
    //                if(Math.abs(even-2*prime) < interval){
    //                    min = Math.min(prime, even-prime);
    //                    max = Math.max(prime, even-prime);
    //                    interval = Math.abs(even-2*prime);
    //                }
    //            }
    //        }
    //
    //        System.out.println(min);
    //        System.out.println(max);
    //    }
    }

  

