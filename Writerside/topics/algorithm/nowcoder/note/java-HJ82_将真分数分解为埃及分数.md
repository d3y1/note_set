# java-HJ82 将真分数分解为埃及分数


    import java.util.Scanner;
    
    public class Main {
        private static StringBuilder result = new StringBuilder();
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                String[] fraction = in.nextLine().trim().split("/");
                // 分子
                Integer a = Integer.parseInt(fraction[0]);
                // 分母
                Integer b = Integer.parseInt(fraction[1]);
    
                result = new StringBuilder();
    
                solution(a, b);
            }
        }
    
        /**
         * 递归
         * @param a
         * @param b
         */
        private static void solution(Integer a, Integer b){
            egypt(a, b);
    
            System.out.println(result);
        }
    
        /**
         * 数学法: 真分数 -> 埃及分数
         * 
         * 算法:
         * 设某个真分数的分子为a, 分母为b;
         * 把c=(b/a+1)作为分解式中第一个埃及分数的分母;
         * 将a-b%a 或 a*c-b作为新的a;
         * 将b*c作为新的b;
         * 
         * 如果a=1, 则最后一个埃及分数为1/b, 算法结束;
         * 如果a>1 && b%a=0, 则最后一个埃及分数为1/(b/a), 算法结束;
         * 否则重复上面的步骤.
         * 
         * 优化: 当b%(a-1)=0时, a/b=1/(b/(a−1))+1/b, 则最后两个埃及分数为1/(b/(a-1))和1/b, 算法结束;
         * 
         * @param a   分子
         * @param b   分母
         */
        private static void egypt(Integer a, Integer b){
            // a=1 则最后一个埃及分数为1/b
            if(a == 1){
                result.append("1/"+b);
                return;
            }
    
            // a>1 && b%a=0 则最后一个埃及分数为1/(b/a)
            if(b%a == 0){
                result.append("1/"+b/a);
                return;
            }
    
            // b%(a-1)=0 则最后两个埃及分数为1/(b/(a-1))和1/b
            if(b%(a-1) == 0){
                result.append("1/"+b/(a-1)+"+1/"+b);
                return;
            }
    
            // 埃及分数的分母
            int c = b/a+1;
            result.append("1/"+c+"+");
            egypt(a-b%a, b*c);
            // egypt(a*c-b, b*c);
        }
    }

  

