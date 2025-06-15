# java-HJ25 数据分类处理


    import java.util.HashMap;
    import java.util.HashSet;
    import java.util.Scanner;
    import java.util.TreeMap;
    import java.util.TreeSet;
    import java.util.Map;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                solution2(in);
            }
        }
    
    
        /**
         * TreeSet + StringBuilder
         * @param in
         */
        private static void solution1(Scanner in){
            int INum = in.nextInt();
            long[] ISeq = new long[INum];
    
            for(int i=0; i<INum; i++){
                ISeq[i] = in.nextLong();
            }
    
            int RNum = in.nextInt();
            // 过滤重复且排序
            TreeSet<Long> RSet = new TreeSet<>();
    
            for(int i=0; i<RNum; i++){
                RSet.add(in.nextLong());
            }
    
            int total = 0;
            StringBuilder result = new StringBuilder();
            for(Long Ri: RSet){
                int count = 0;
                StringBuilder sb = new StringBuilder();
                for(int k=0; k<INum; k++){
                    if(String.valueOf(ISeq[k]).contains(String.valueOf(Ri))){
                        count++;
                        sb.append(k+" "+ISeq[k]+" ");
                    }
                }
                if(count > 0){
                    result.append(Ri+" "+count+" ");
                    result.append(sb);
                    total += 2+count*2;
                }
            }
    
            result.insert(0, total+" ");
    
            System.out.println(result);
        }
    
    
        /**
         * HashSet + TreeMap + HashMap
         * @param in
         */
        private static void solution2(Scanner in){
            int INum = in.nextInt();
            long[] ISeq = new long[INum];
    
            for(int i=0; i<INum; i++){
                ISeq[i] = in.nextLong();
            }
    
            int RNum = in.nextInt();
            // 过滤重复
            HashSet<Long> RSet = new HashSet<>();
    
            for(int i=0; i<RNum; i++){
                RSet.add(in.nextLong());
            }
    
            // Ri -> 个数
            TreeMap<Long, Integer> RCountMap = new TreeMap<>();
            // Ri -> 位置及值
            HashMap<Long, String> RIndexValueMap = new HashMap<>();
            for(Long Ri: RSet){
                for(int k=0; k<INum; k++){
                    if(String.valueOf(ISeq[k]).contains(String.valueOf(Ri))){
                        RCountMap.put(Ri, RCountMap.getOrDefault(Ri, 0)+1);
                        if(RIndexValueMap.get(Ri) != null){
                            RIndexValueMap.put(Ri, RIndexValueMap.get(Ri)+k+" "+ISeq[k]+" ");
                        }else{
                            RIndexValueMap.put(Ri, k+" "+ISeq[k]+" ");
                        }
                    }
                }
            }
    
            int total = RCountMap.size() * 2;
            for(int count: RCountMap.values()){
                total += count * 2;
            }
    
            StringBuilder result = new StringBuilder(total+" ");
            for(Map.Entry<Long, Integer> entry: RCountMap.entrySet()){
                result.append(entry.getKey()+" "+entry.getValue()+" ");
                result.append(RIndexValueMap.get(entry.getKey()));
            }
    
            System.out.println(result);
        }
    }

  

