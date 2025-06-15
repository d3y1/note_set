# java-HJ54 表达式求值


    import java.util.Scanner;
    import java.util.Stack;
    import javax.script.ScriptEngine;
    import javax.script.ScriptEngineManager;
    import javax.script.ScriptException;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String input = in.nextLine();
    
            int result = solve(input);
    
            System.out.print(result);
    
        }
    
        private static int solve(String input) {
            Stack<Integer> stack = new Stack<>();
            int n = input.length();
            char[] chs = input.toCharArray();
            //初始化符号为'+'
            char sign = '+';
            //记录数字
            int number = 0;
            for (int i = 0; i < n; i++) {
                char ch = chs[i];
                //当前字符是空格，跳过
                if (ch == ' ') {
                    continue;
                }
                //当前字符是数字，拼数字
                if (Character.isDigit(ch)) {
                    number = number * 10 + ch - '0';
                }
                //如果当前字符是小括号
                if (ch == '(') {
                    //移到小括号后一位字符
                    int j = i + 1;
                    //统计括号的数量
                    int count = 1;
                    while (count > 0) {
                        //遇到右括号，括号数-1
                        if (chs[j] == ')') {
                            count--;
                        }
                        //遇到左括号，括号数+1
                        if (chs[j] == '(') {
                            count++;
                        }
                        j++;
                    }
                    //递归，解小括号中的表达式
                    number = solve(input.substring(i + 1, j - 1));
                    i = j - 1;
                }
                //遇到符号，将数字处理后放进栈
                if (!Character.isDigit(ch) || i == n - 1) {
                    //如果是'+',直接入栈
                    if (sign == '+') {
                        stack.push(number);
                    }
                    //如果是'-',数字取相反数在入栈
                    else if (sign == '-') {
                        stack.push(-1 * number);
                    }
                    //如果是'*',弹出一个数字乘后放入栈
                    else if (sign == '*') {
                        stack.push(stack.pop() * number);
                    }
                    //如果是'/',弹出一个数字/后放入栈
                    else if (sign == '/') {
                        stack.push(stack.pop() / number);
                    }
                    //更新符号
                    sign = ch;
                    //刷新数字
                    number = 0;
                }
            }
            //栈中数字求和得到结果
            int ans = 0;
            while (!stack.isEmpty()) {
                ans += stack.pop();
            }
            return ans;
        }
    
    
        // public static void main(String[] args) throws ScriptException{
        //     Scanner in = new Scanner(System.in);
    
        //     String input = in.nextLine();
            
        //     ScriptEngine scriptEngine = new ScriptEngineManager().getEngineByName("nashorn");
        //     System.out.println(scriptEngine.eval(input));
        // }
    }

  

