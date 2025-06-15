# java-HJ105 记负均正II


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            int nonNegCount = 0;
            int negCount = 0;
            float total = 0;
    
            while (in.hasNextInt()){
                int num = in.nextInt();
                if(num >= 0){
                    nonNegCount++;
                    total += num;
                }else {
                    negCount++;
                }
            }
    
    
            System.out.println(negCount);
            if(nonNegCount == 0){
                System.out.print("0.0");
            }else{
                float average = total/nonNegCount;
                System.out.printf("%.1f", average);
            }
        }
    }

  

