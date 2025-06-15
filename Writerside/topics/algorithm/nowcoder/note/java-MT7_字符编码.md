# java-MT7 字符编码


    import java.util.HashMap;
    import java.util.Map;
    import java.util.PriorityQueue;
    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()) {
                solution(in);
            }
        }
    
        /**
         * 优先队列: 哈夫曼编码
         * @param in
         */
        private static void solution(Scanner in){
            String str = in.nextLine();
    
            Map<Character, Integer> charCountMap = new HashMap<>();
            for(char ch: str.toCharArray()){
                charCountMap.put(ch, charCountMap.getOrDefault(ch, 0)+1);
            }
    
            PriorityQueue<Integer> queue = new PriorityQueue<>();
            for(int value : charCountMap.values()){
                queue.offer(value);
            }
    
            int result = 0;
            while(queue.size() >= 2) {
                int a = queue.poll();
                int b = queue.poll();
                result += a+b;
                queue.offer(a+b);
            }
    
            System.out.println(result);
        }
    }

  

