# java-HJ6 质数因子


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
            int num = in.nextInt();
    
            int i = 2;
    
            while(i*i <= num){
                if(num%i == 0){
                    System.out.print(i+" ");
                    num /= i;
                }else{
                    i++;
                }
            }
            System.out.print(num);
        }
    }

  

