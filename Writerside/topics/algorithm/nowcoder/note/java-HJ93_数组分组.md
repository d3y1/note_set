# java-HJ93 数组分组


    import java.util.ArrayList;
    import java.util.List;
    import java.util.Scanner;
    
    public class Main {
        private static boolean[] isVisited;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法
         * @param in
         */
        private static void solution(Scanner in){
            int N = in.nextInt();
    
            int group3Sum = 0;
            int group5Sum = 0;
            int sum = 0;
            List<Integer> list = new ArrayList<>();
            for(int i=0; i<N; i++){
                int num = in.nextInt();
                if(num%5 == 0){
                    group5Sum += num;
                }else if(num%3 == 0){
                    group3Sum += num;
                }else{
                    list.add(num);
                }
                sum += num;
            }
    
            // 总和奇数
            if(sum%2 != 0){
                System.out.println(false);
            }else{
                Integer[] array = list.toArray(new Integer[0]);
                isVisited = new boolean[array.length];
    
                boolean isEqual = operate(0, group3Sum, group5Sum, array);
    
                if(isEqual){
                    System.out.println(true);
                }else{
                    System.out.println(false);
                }
            }
        }
    
        /**
         * 递归
         * @param opTimes
         * @param group3Sum
         * @param group5Sum
         * @param array
         * @return
         */
        private static boolean operate(int opTimes, int group3Sum, int group5Sum, Integer[] array){
            if(opTimes == array.length){
                if(group3Sum == group5Sum){
                    return true;
                }
                return false;
            }
    
            for(int i=0; i<array.length; i++){
                if(!isVisited[i]){
                    isVisited[i] = true;
    
                    if(operate(opTimes+1, group3Sum+array[i], group5Sum, array) || operate(opTimes+1, group3Sum, group5Sum+array[i], array)){
                        return true;
                    }
    
                    isVisited[i] = false;
                }
            }
    
            return false;
        }
    }

  

