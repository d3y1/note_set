# java-MT5 字符串计数


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in =  new Scanner(System.in);
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法: 进制转化
         * @param in
         */
        private static void solution(Scanner in){
            String s1 = in.next();
            String s2 = in.next();
            int len1 = in.nextInt();
            int len2 = in.nextInt();
    
            // 起始位 补a
            for(int i=s1.length(); i<len2; i++){
                s1 += 'a';
            }
            // 结束位 补'z'+1
            for(int i=s2.length(); i<len2; i++){
                s2 += 'z'+1;
            }
    
            // 记录两个字符串对应位相减的值 比如s1补位后为aba s2补位后为ce('z'+1) gap数组记录的值是{2, 3, 26}
            int[] gap = new int[len2];
            for(int i=0; i<len2; i++){
                gap[i] = s2.charAt(i)-s1.charAt(i);
            }
    
            int sum = 0;
            // 从长度len1开始，依次计算每个长度下的字符串个数，这里能取到len2
            for(int i=len1; i<=len2; i++){
                // gap数组中是{2, 3}, len为2时，就是2*Math.pow(26,1)+3*Math.pow(26,0)。
                for(int j=0; j<i; j++){
                    sum += gap[j]*Math.pow(26,i-1-j);
                }
            }
    
            System.out.println((sum-1)%1000007);
        }
    }

  

