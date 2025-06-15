# java-MT41 射击训练


    import java.util.Arrays;
    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法: 统计个数
         * @param in
         */
        private static void solution(Scanner in){
            int n = in.nextInt();
    
            int[] scores = new int[n];
            int[] count = new int[1001];
    
            for(int i=0; i<n; i++){
                scores[i] = in.nextInt();
                count[scores[i]]++;
            }
    
            Arrays.sort(scores);
    
            int multi;
            int result = 0;
            for(int i=0; i<n; i++){
                for(int j=i+1; j<n; j++){
                    for(int k=j+1; k<n; k++){
                        multi = scores[i]*scores[j]*scores[k];
                        if(multi > 1000){
                            break;
                        }else{
                            count[scores[i]]--;
                            count[scores[j]]--;
                            count[scores[k]]--;
                            if(count[multi] > 0){
                                result++;
                            }
                            count[scores[i]]++;
                            count[scores[j]]++;
                            count[scores[k]]++;
                        }
                    }
                }
            }
    
            System.out.println(result);
        }
    }

  

