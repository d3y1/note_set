# java-HJ94 记票统计


    import java.util.HashMap;
    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            HashMap<String, Integer> rateMap = new HashMap<>();
            int invalidCount = 0;
    
            int peopleNum = in.nextInt();
            String[] nameArray = new String[peopleNum];
            for(int i=0; i<peopleNum; i++){
                String people = in.next();
                rateMap.put(people, 0);
                nameArray[i] = people;
            }
    
            int peopleVote = in.nextInt();
            for(int i=1; i<=peopleVote; i++){
                String ticket = in.next();
                if(rateMap.containsKey(ticket)){
                    rateMap.put(ticket, rateMap.get(ticket)+1);
                }else{
                    invalidCount++;
                }
            }
    
    //        for(String key: rateMap.keySet()){
    //            System.out.println(key +" : "+rateMap.get(key));
    //        }
    //        for(String people: nameArray){
    //            System.out.println(people +" : "+rateMap.get(people));
    //        }
    //
    //        System.out.println("Invalid : "+invalidCount);
    
    
            StringBuilder result = new StringBuilder();
            for(String people: nameArray){
                result.append(people);
                result.append(" : ");
                result.append(rateMap.get(people));
                result.append("\n");
            }
            result.append("Invalid : ");
            result.append(invalidCount);
            System.out.println(result);
        }
    
    
    
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        int people = Integer.valueOf(in.nextLine());
    //        String names = in.nextLine();
    //        String[] nameArray = names.split(" ");
    //
    //        int peopleRate = Integer.valueOf(in.nextLine());
    //        String namesRate = in.nextLine();
    //        String[] nameRateArray = namesRate.split(" ");
    //
    //        int invalidCount = 0;
    //
    //        HashMap<String, Integer> rateMap = new HashMap<>();
    //        for(int i=0; i<people; i++){
    //            rateMap.put(nameArray[i], 0);
    //        }
    //
    //        for(int i=0; i<peopleRate; i++){
    //            if(rateMap.get(nameRateArray[i]) != null){
    //                rateMap.put(nameRateArray[i], rateMap.get(nameRateArray[i])+1);
    //            }else{
    //                invalidCount++;
    //            }
    //        }
    //
    //        for(int i=0; i<people; i++){
    //            System.out.println(nameArray[i]+" : "+rateMap.get(nameArray[i]));
    //        }
    //
    //        System.out.println("Invalid : "+invalidCount);
    //    }
    }

  

