# java-NC402 包含不超过两种字符的最长子串


    import java.util.Scanner;
    
    /**
     * NC402 包含不超过两种字符的最长子串
     * @author d3y1
     */
    public class Main {
        // 字符种数
        private static final int K = 2;
        
        public static void main(String[] args) {
            solution();
        }
    
        /**
         * 贪心+双指针(毛毛虫)
         * 
         * 相似 -> NC41 最长无重复子数组            [nowcoder]
         * 相似 -> NC170 最长不含重复字符的子字符串   [nowcoder]
         * 相似 -> NC356 至多包含K种字符的子串       [nowcoder]
         * 相似 -> NC387 找到字符串中的异位词        [nowcoder]
         */
        private static void solution(){
            Scanner in = new Scanner(System.in);
            char[] chars = in.nextLine().toCharArray();
    
            int n = chars.length;
            if(n <= K){
                System.out.println(n);
                return;
            }
    
            int result = 0;
            int[] cnt = new int[26];
            int kind = 0;
            // 双指针 毛毛虫
            for(int i=0,j=0; i<=j&&j<n; j++){
                // 贪心
                if(cnt[chars[j]-'a']++ == 0){
                    kind++;
                }
    
                while(kind > K){
                    if(--cnt[chars[i++]-'a'] == 0){
                        kind--;
                    }
                }
    
                result = Math.max(result, j-i+1);
            }
    
            System.out.println(result);
        }
    }

  

