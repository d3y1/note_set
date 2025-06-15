# java-QQ8 数字转换机


    import java.util.Scanner;
    
    public class Main {
        // 默认不能完成转换
        private static int result = -1;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法: DFS遍历所有情况
         * @param in
         */
        private static void solution(Scanner in){
            int a = in.nextInt();
            int b = in.nextInt();
            int A = in.nextInt();
            int B = in.nextInt();
    
            dfs(a, b, A, B, 0);
    
            System.out.println(result);
        }
    
        /**
         * DFS
         * @param a
         * @param b
         * @param A
         * @param B
         * @param ops
         */
        private static void dfs(int a, int b, int A, int B, int ops){
            // 不能完成转换
            if(a>A || b>B){
                return;
            }
    
            // 完成转换 更新次数
            if(a==A && b==B){
                if(result == -1){
                    result = ops;
                }else{
                    result = Math.min(result, ops);
                }
    
                return;
            }
    
            // 红色按钮
            dfs(a+1, b+1, A, B, ops+1);
            // 蓝色按钮
            dfs(a*2, b*2, A, B, ops+1);
        }
    }

  

