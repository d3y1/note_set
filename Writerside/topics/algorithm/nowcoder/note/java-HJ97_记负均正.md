# java-HJ97 记负均正


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            int n = in.nextInt();
            in.hasNextLine();
    
            int posCount = 0;
            int negCount = 0;
            float posTotal = 0;
    
            for(int i=1; i<=n; i++){
                int num = in.nextInt();
                if(num > 0){
                    posCount++;
                    posTotal += num;
                }else if(num < 0){
                    negCount++;
                }
            }
    
    
            System.out.print(negCount+" ");
            if(posCount == 0){
                System.out.print("0.0");
            }else{
                float average = posTotal/posCount;
                System.out.printf("%.1f", average);
            }
        }
    }

  

