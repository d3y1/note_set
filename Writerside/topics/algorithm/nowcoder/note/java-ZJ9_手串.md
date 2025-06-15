# java-ZJ9 手串


    import java.util.ArrayList;
    import java.util.Collections;
    import java.util.HashMap;
    import java.util.List;
    import java.util.Scanner;
    
    public class Main {
        private static int num;
        private static int series;
        private static final int times = 2;
        private static HashMap<Integer, List<Integer>> colourLocMap = new HashMap<>();
    
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
            num = in.nextInt();
            series = in.nextInt();
            int colours = in.nextInt();
    
            int kinds;
            for(int i=1; i<=num; i++){
                kinds = in.nextInt();
                int colour;
                List<Integer> list;
                for(int j=1; j<=kinds; j++){
                    colour = in.nextInt();
                    list = colourLocMap.get(colour);
                    if(list != null){
                        list.add(i);
                        colourLocMap.put(colour, list);
                    }else{
                        colourLocMap.put(colour, new ArrayList<>(Collections.singletonList(i)));
                    }
                }
            }
    
            int result = 0;
            for(int i=1; i<=colours; i++){
                if(!isColourOk(i)){
                    result++;
                }
            }
    
            System.out.println(result);
        }
    
        private static boolean isColourOk(int colour){
            // locations有序(从小到大)
            List<Integer> locations = colourLocMap.get(colour);
    
            // 任何珠子都没涂该颜色
            if(locations != null){
                int size = locations.size();
                if(size >= times){
                    for(int i=1; i<size; i++){
                        if(locations.get((i-1)%size)+series-1 >= locations.get(i%size)){
                            return false;
                        }
                    }
    
                    if((locations.get(size-1)+series-1)%num >= locations.get(0)){
                        return false;
                    }
                }
            }
            return true;
        }
    }

  

