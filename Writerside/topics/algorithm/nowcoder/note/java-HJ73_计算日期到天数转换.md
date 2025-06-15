# java-HJ73 计算日期到天数转换


    import java.util.Calendar;
    import java.util.HashMap;
    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
    
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while (in.hasNextInt()){
                int year = in.nextInt();
                int month = in.nextInt();
                int day = in.nextInt();
    
                Calendar calendar = Calendar.getInstance();
                calendar.set(year, month-1, day);
    
                System.out.println(calendar.get(Calendar.DAY_OF_YEAR));
            }
        }
    
    
    
        // public static void main(String[] args) {
        //     Scanner in = new Scanner(System.in);
            
        //     int[] monthDays = new int[]{31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30};
            
        //     while (in.hasNextInt()){
        //         int year = in.nextInt();
        //         int month = in.nextInt();
        //         int day = in.nextInt();
    
        //         int days = day;
        //         for(int i=0; i<month-1; i++){
        //             days += monthDays[i];
        //         }
    
        //         if(month>2 && isLeapYear(year)){
        //             days++;
        //         }
    
        //         System.out.println(days);
        //     }
        // }
    
    
    
        // private static HashMap<Integer, Integer> monthDaysMap = new HashMap<Integer, Integer>();
        
        // static {
        //     monthDaysMap.put(0, 0);
        //     monthDaysMap.put(1, 31);
        //     monthDaysMap.put(2, 31+28);
        //     monthDaysMap.put(3, 31+28+31);
        //     monthDaysMap.put(4, 31+28+31+30);
        //     monthDaysMap.put(5, 31+28+31+30+31);
        //     monthDaysMap.put(6, 31+28+31+30+31+30);
        //     monthDaysMap.put(7, 31+28+31+30+31+30+31);
        //     monthDaysMap.put(8, 31+28+31+30+31+30+31+31);
        //     monthDaysMap.put(9, 31+28+31+30+31+30+31+31+30);
        //     monthDaysMap.put(10, 31+28+31+30+31+30+31+31+30+31);
        //     monthDaysMap.put(11, 31+28+31+30+31+30+31+31+30+31+30);
        // }
    
        // public static void main(String[] args) {
        //     Scanner in = new Scanner(System.in);
    
        //     while (in.hasNextInt()){
        //         int year = in.nextInt();
        //         int month = in.nextInt();
        //         int day = in.nextInt();
    
        //         int days = monthDaysMap.get(month-1)+day;
    
        //         if(month>2 && isLeapYear(year)){
        //             days++;
        //         }
    
        //         System.out.println(days);
        //     }
        // }
        
        private static boolean isLeapYear(int year){
            if(year%4==0 && year%100!=0){
                return true;
            }
            
            if(year%400 == 0){
                return true;
            }
            
            return false;
        }
    }

  

