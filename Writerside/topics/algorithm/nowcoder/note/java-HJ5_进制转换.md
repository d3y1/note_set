# java - HJ5 进制转换


    import java.util.HashMap;
    import java.util.Map;
    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
    
        private static final int BASE = 16;
    
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String inputLine = in.nextLine();
    
            // System.out.println(Integer.parseInt(inputLine.substring(2), 16));
            System.out.println(exchange(inputLine.substring(2)));
        }
    
        private static Integer exchange(String input) {
    
            int index = 0;
            int result = 0;
            int hexTimes = input.length();
            while (index < input.length()) {
                result = result * BASE + map.get(input.charAt(index));
                index++;
            }
    
            return result;
        }
    
        // private static Integer exchange(String input) {
    
        //     int index = 0;
        //     int result = 0;
        //     int hexTimes = input.length();
        //     while (index < input.length()) {
        //         result += charToNum(input.charAt(index)) * Math.pow(16, --hexTimes);
        //         index++;
        //     }
    
        //     return result;
        // }
    
        private static Map<Character, Integer> map = new HashMap<Character, Integer>() {
            {
                put('0', 0);
                put('1', 1);
                put('2', 2);
                put('3', 3);
                put('4', 4);
                put('5', 5);
                put('6', 6);
                put('7', 7);
                put('8', 8);
                put('9', 9);
                put('A', 10);
                put('B', 11);
                put('C', 12);
                put('D', 13);
                put('E', 14);
                put('F', 15);
                put('a', 10);
                put('b', 11);
                put('c', 12);
                put('d', 13);
                put('e', 14);
                put('f', 15);
            }
        };
    
        // private static int charToNum(char hexChar) {
        //     int result = 0;
    
        //     switch (hexChar) {
        //         case 'A': {
        //                 result = 10;
        //                 break;
        //             }
        //         case 'B': {
        //                 result = 11;
        //                 break;
        //             }
        //         case 'C': {
        //                 result = 12;
        //                 break;
        //             }
        //         case 'D': {
        //                 result = 13;
        //                 break;
        //             }
        //         case 'E': {
        //                 result = 14;
        //                 break;
        //             }
        //         case 'F': {
        //                 result = 15;
        //                 break;
        //             }
        //         default:
        //             result =  Character.getNumericValue(hexChar);
        //     }
    
        //     return result;
        // }
    }

  

