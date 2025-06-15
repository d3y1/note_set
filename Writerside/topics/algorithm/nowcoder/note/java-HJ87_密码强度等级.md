# java-HJ87 密码强度等级


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        private static final int VERY_SECURE = 90;
        private static final int SECURE = 80;
        private static final int VERY_STRONG = 70;
        private static final int STRONG = 60;
        private static final int AVERAGE = 50;
        private static final int WEAK = 25;
        private static final int VERY_WEAK = 0;
    
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String input = in.nextLine();
            char[] inputChars = input.toCharArray();
    
            int len = input.length();
            int digitCount = 0;
            int upperCount = 0;
            int lowerCount = 0;
            int symbolCount = 0;
            int score = 0;
    
            for(char aChar: inputChars){
    //            if('0'<=aChar && aChar<='9'){
                if(Character.isDigit(aChar)){
                    digitCount++;
    //            }else if('a'<=aChar && aChar<='z') {
                }else if(Character.isLowerCase(aChar)) {
                    lowerCount++;
    //            }else if('A'<=aChar && aChar<='Z') {
                }else if(Character.isUpperCase(aChar)) {
                    upperCount++;
                }else{
                    symbolCount++;
                }
            }
    
            // 1
            if(len <= 4){
                score += 5;
            }else if(len <= 7){
                score += 10;
            }else{
                score += 25;
            }
    
            // 2
            if(upperCount>0 && lowerCount>0){
                score += 20;
            }else if(upperCount>0 || lowerCount>0){
                score += 10;
            }
    
            // 3
            if(digitCount > 1){
                score += 20;
            }else if(digitCount == 1){
                score += 10;
            }
    
            // 4
            if(symbolCount > 1){
                score += 25;
            }else if(symbolCount == 1){
                score += 10;
            }
    
            // 5
            if(digitCount >= 1){
                if(symbolCount >= 1){
                    if(upperCount>=1 && lowerCount>=1){
                        score += 5;
                    }else if(upperCount>=1 || lowerCount>=1){
                        score += 3;
                    }
                }else{
                    if(upperCount>=1 || lowerCount>=1){
                        score += 2;
                    }
                }
            }
    
            if(score >= VERY_SECURE){
                System.out.print("VERY_SECURE");
            }else if(score >= SECURE){
                System.out.print("SECURE");
            }else if(score >= VERY_STRONG){
                System.out.print("VERY_STRONG");
            }else if(score >= STRONG){
                System.out.print("STRONG");
            }else if(score >= AVERAGE){
                System.out.print("AVERAGE");
            }else if(score >= WEAK){
                System.out.print("WEAK");
            }else if(score >= VERY_WEAK){
                System.out.print("VERY_WEAK");
            }
        }
    }

  

