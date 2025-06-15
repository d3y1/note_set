# java-HJ50 四则运算

```java
import java.util.Scanner;
import java.util.Stack;

public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);

        while (in.hasNext()){
            String mathStr = in.nextLine();

//            int result = solution1(mathStr);
            int result = solution2(mathStr);

            System.out.println(result);
        }
    }

    private static int solution1(String mathStr) {
        Stack<Integer> stack = new Stack<>();
        int len = mathStr.length();
        char[] chars = mathStr.toCharArray();
        // 初始化符号为'+'
        char sign = '+';
        // 记录数字
        int number = 0;
        for (int i = 0; i < len; i++) {
            char aChar = chars[i];
            // 1 当前字符是数字 拼数字
            if (Character.isDigit(aChar)) {
                number = number * 10 + aChar - '0';
            }

            // 2 当前字符是大括号
            if (aChar == '{') {
                // 移到大括号后一位字符
                int j = i + 1;
                // 统计大括号的数量
                int count = 1;
                while (count > 0) {
                    // 遇到右括号 括号数-1
                    if (chars[j] == '}') {
                        count--;
                    }
                    // 遇到左括号 括号数+1
                    if (chars[j] == '{') {
                        count++;
                    }
                    j++;
                }
                // 递归 解大括号中的表达式
                number = solution1(mathStr.substring(i + 1, j - 1));
                i = j - 1;
            }

            // 3 当前字符是中括号
            if (aChar == '[') {
                // 移到中括号后一位字符
                int j = i + 1;
                // 统计中括号的数量
                int count = 1;
                while (count > 0) {
                    // 遇到右括号 括号数-1
                    if (chars[j] == ']') {
                        count--;
                    }
                    // 遇到左括号 括号数+1
                    if (chars[j] == '[') {
                        count++;
                    }
                    j++;
                }
                // 递归 解中括号中的表达式
                number = solution1(mathStr.substring(i + 1, j - 1));
                i = j - 1;
            }


            // 4 当前字符是小括号
            if (aChar == '(') {
                // 移到小括号后一位字符
                int j = i + 1;
                // 统计小括号的数量
                int count = 1;
                while (count > 0) {
                    // 遇到右括号 括号数-1
                    if (chars[j] == ')') {
                        count--;
                    }
                    // 遇到左括号 括号数+1
                    if (chars[j] == '(') {
                        count++;
                    }
                    j++;
                }
                // 递归 解小括号中的表达式
                number = solution1(mathStr.substring(i + 1, j - 1));
                i = j - 1;
            }

            // 5 当前字符是运算符号 将数字处理后放进栈
            if (!Character.isDigit(aChar) || i == len - 1) {
                // '+' 直接入栈
                if (sign == '+') {
                    stack.push(number);
                }
                // '-' 数字取反数再入栈
                else if (sign == '-') {
                    stack.push(-1 * number);
                }
                // '*' 弹出一个数字相乘后再放入栈
                else if (sign == '*') {
                    stack.push(stack.pop() * number);
                }
                // '/' 弹出一个数字相除后再放入栈
                else if (sign == '/') {
                    stack.push(stack.pop() / number);
                }
                // 更新符号
                sign = aChar;
                // 刷新数字
                number = 0;
            }
        }
        // 栈中数字求和得到结果
        int ans = 0;
        while (!stack.isEmpty()) {
            ans += stack.pop();
        }
        return ans;
    }


    private static int solution2(String mathStr) {
        mathStr = mathStr.replace("[", "(");
        mathStr = mathStr.replace("]", ")");
        mathStr = mathStr.replace("{", "(");
        mathStr = mathStr.replace("}", ")");
        Stack<Integer> stack = new Stack<>();
        int len = mathStr.length();
        char[] chars = mathStr.toCharArray();
        // 初始化符号为'+'
        char sign = '+';
        // 记录数字
        int number = 0;
        for (int i = 0; i < len; i++) {
            char aChar = chars[i];
            // 1 当前字符是数字 拼数字
            if (Character.isDigit(aChar)) {
                number = number * 10 + aChar - '0';
            }

            // 2 当前字符是小括号
            if (aChar == '(') {
                // 移到小括号后一位字符
                int j = i + 1;
                // 统计小括号的数量
                int count = 1;
                while (count > 0) {
                    // 遇到右括号 括号数-1
                    if (chars[j] == ')') {
                        count--;
                    }
                    // 遇到左括号 括号数+1
                    if (chars[j] == '(') {
                        count++;
                    }
                    j++;
                }
                // 递归 解小括号中的表达式
                number = solution2(mathStr.substring(i + 1, j - 1));
                i = j - 1;
            }

            // 3 当前字符是运算符号 将数字处理后放进栈
            if (!Character.isDigit(aChar) || i == len - 1) {
                // '+' 直接入栈
                if (sign == '+') {
                    stack.push(number);
                }
                // '-' 数字取反数再入栈
                else if (sign == '-') {
                    stack.push(-1 * number);
                }
                // '*' 弹出一个数字相乘后再放入栈
                else if (sign == '*') {
                    stack.push(stack.pop() * number);
                }
                // '/' 弹出一个数字相除后再放入栈
                else if (sign == '/') {
                    stack.push(stack.pop() / number);
                }
                // 更新符号
                sign = aChar;
                // 刷新数字
                number = 0;
            }
        }
        // 栈中数字求和得到结果
        int ans = 0;
        while (!stack.isEmpty()) {
            ans += stack.pop();
        }
        return ans;
    }
}
```
