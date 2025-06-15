# java-HJ107 求解立方根


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        private static void solution(Scanner in){
            double val = in.nextDouble();
            double num = Math.abs(val);
    
            double result = getCubeRoot(num);
            
            if(val < 0){
                result = -result;
            }
    
            System.out.println(result);
        }
    
        /**
         * 二分法
         * @param num
         * @return
         */
        private static double getCubeRoot(double num){
    
            if(num == 0){
                return 0;
            }
    
            double l = 0.0;
            double r = 3.0;
            while(l+0.1 <= r){
                double mid = (l+r)/2;
                if(mid*mid*mid >= num) {
                    r = mid;
                }else{
                    l = mid;
                }
            }
            
            double result;
            l = Double.parseDouble(String.format("%.1f", l));
            r = Double.parseDouble(String.format("%.1f", r));
    
            if(Math.abs(num-l*l*l) <= Math.abs(num-r*r*r)){
                result = l;
            }else{
                result = r;
            }
    
            return result;
        }
    }

  

