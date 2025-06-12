# MP3光标位置
https://www.nowcoder.com/practice/eaf5b886bd6645dd9cfb5406f3753e15

    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while (in.hasNext()){
                String total = in.nextLine();
                String ops = in.nextLine();
    
                solution(Integer.parseInt(total), ops);
            }
        }
    
        /**
         * 模拟法
         * @param total
         * @param ops
         */
        private static void solution(int total, String ops){
    
            // 光标当前位置
            int currIndex = 1;
            // 当前页第一位置
            int firstIndex = 1;
    
            // 歌曲总数<=4
            if(total <= 4){
                for(char op: ops.toCharArray()){
                    if(op == 'U'){
                        if(currIndex == 1){
                            currIndex = total;
                        }else{
                            currIndex--;
                        }
                    }else if(op == 'D'){
                        if(currIndex == total){
                            currIndex = 1;
                        }else{
                            currIndex++;
                        }
                    }
                }
    
                for(int i=1; i<=total; i++){
                    System.out.print(i+" ");
                }
            }
            // 歌曲总数大于4
            else{
                for(char op: ops.toCharArray()){
                    if(op == 'U'){
                        // 光标在第一首歌曲上
                        if(currIndex == 1){
                            currIndex = total;
                            firstIndex = total-3;
                        }else{
                            if(currIndex == firstIndex){
                                currIndex--;
                                firstIndex--;
                            }else{
                                currIndex--;
                            }
                        }
                    }else if(op == 'D'){
                        // 光标在最后一首歌上
                        if(currIndex == total){
                            currIndex = 1;
                            firstIndex = 1;
                        }else{
                            if(currIndex-firstIndex==3 && firstIndex < total-3){
                                currIndex++;
                                firstIndex++;
                            }else{
                                currIndex++;
                            }
                        }
                    }
                }
    
                for(int i=firstIndex; i<=Math.min(firstIndex+3, total); i++){
                    System.out.print(i+" ");
                }
            }
            System.out.println();
            System.out.println(currIndex);
        }
    }
    

