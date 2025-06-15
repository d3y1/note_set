# java-HJ19 简单错误记录


    import java.util.HashMap;
    import java.util.HashSet;
    import java.util.LinkedHashMap;
    import java.util.LinkedList;
    import java.util.Map;
    import java.util.Queue;
    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            solution1(in);
            solution2(in);
        }
    
    
        /**
         * LinkedHashMap 有序
         * @param in
         */
        private static void solution1(Scanner in){
            HashMap<String, Integer> map = new LinkedHashMap<>();
    
            while(in.hasNext()){
                String record = in.nextLine().trim();
    
                String[] fileLine = record.split("\\s+");
                String[] fileParts = fileLine[0].split("\\\\");
                String fileLastPart = fileParts[fileParts.length-1];
    
                String fileSuffix = fileLastPart.substring(Math.max(fileLastPart.length()-16, 0));
                String line = fileLine[1];
    
                String key = fileSuffix + " " + line;
                map.put(key, map.getOrDefault(key, 0)+1);
            }
    
            // 输出最后8个
            int pre = 0;
            for(Map.Entry<String, Integer> entry: map.entrySet()){
                if(map.size()-pre <= 8){
                    System.out.println(entry.getKey() + " " + entry.getValue());
                }
                pre++;
            }
        }
    
    
        /**
         * map set queue
         * @param in
         */
        private static void solution2(Scanner in){
            HashSet<String> set = new HashSet<>();
            Queue<String> queue = new LinkedList<>();
            HashMap<String, Integer> map = new HashMap<>();
    
            while(in.hasNext()){
                String record = in.nextLine().trim();
    
                // duplicate record
                if(set.contains(record)){
                    continue;
                }else{
                    set.add(record);
                }
                
                String[] fileLine = record.split(" ");
                String[] fileParts = fileLine[0].split("\\\\");
                String fileLastPart = fileParts[fileParts.length-1];
    
                String fileSuffix = fileLastPart.substring(Math.max(fileLastPart.length()-16, 0));
                String line = fileLine[1];
    
                String key = fileSuffix + " " + line;
    
                if(map.containsKey(key)){
                    map.put(key, map.get(key)+1);
                }else{
                    map.put(key, 1);
    
                    if(queue.size() == 8){
                        queue.poll();
                    }
                    queue.add(key);
                }
            }
    
            for(String key: queue){
                System.out.println(key + " " + map.get(key));
            }
        }
    }

  

