# java-BD8 完成括号匹配


    import java.util.Scanner;
    import java.util.Stack;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法: 栈
         */
        private static void solution(Scanner in){
            String s = in.nextLine();
    
            Stack<Character> stack = new Stack<>();
    
            for(char ch: s.toCharArray()){
                if(ch == '['){
                    stack.push(ch);
                }else{
                    if(!stack.isEmpty()){
                        if(stack.peek() == '['){
                            stack.pop();
                        }else{
                            stack.push(ch);
                        }
                    }else{
                        stack.push(ch);
                    }
                }
            }
    
            StringBuilder sb = new StringBuilder(s);
            char top;
            while(!stack.isEmpty()){
                top = stack.pop();
                if(top == '['){
                    sb.append(']');
                }else{
                    sb.insert(0, '[');
                }
            }
    
            System.out.println(sb);
        }
    }

  

