# java-HJ71 字符串通配符


    import java.util.Scanner;
    
    public class Main {
        private static int indexL = 0;
        private static int indexR = 0;
        private static int targetLen = 0;
    
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                // solution2(in);
                // solution3(in);
            }
        }
    
        /**
         * 动态规划 dp[i][j]表示规则字符串子串rule(0,i)与目标字符串子串target(0,j)是否匹配
         */
        private static void solution1(Scanner in){
            String rule = in.nextLine().toLowerCase();
            String target = in.nextLine().toLowerCase();
    
            int ruleLen = rule.length();
            int targetLen = target.length();
    
            // init dp
            boolean[][] dp = new boolean[ruleLen+1][targetLen+1];
            dp[0][0] = true;
            if(rule.charAt(0) == '*'){
                for(int j=0; j<=targetLen; j++){
                    dp[1][j] = true;
                }
            }
    
            for(int i=1; i<=ruleLen; i++){
                char ruleChar = rule.charAt(i-1);
                for(int j=1; j<=targetLen; j++){
                    char targetChar = target.charAt(j-1);
    
                    boolean targetCharIsLetterOrDigit = Character.isLetter(targetChar) || Character.isDigit(targetChar);
                    if(ruleChar == '?'){
                        if(targetCharIsLetterOrDigit){
                            dp[i][j] = dp[i-1][j-1];
                        }
                    }else if(ruleChar == '*'){
                        if(targetCharIsLetterOrDigit){
                            dp[i][j] = dp[i][j-1] || dp[i-1][j] || dp[i-1][j-1];
                        }
                    }else{
                        if(ruleChar == targetChar){
                            dp[i][j] = dp[i-1][j-1];
                        }
                    }
                }
            }
    
            System.out.println(dp[ruleLen][targetLen]);
        }
    
    
        /**
         * 模拟法 分段匹配
         * @param in
         */
        private static void solution2(Scanner in){
            // limit=-1 保留结尾空串
            String[] rules = in.nextLine().toLowerCase().split("[*]+", -1);
            String target = in.nextLine().toLowerCase();
            targetLen = target.length();
            indexL = 0;
            indexR = target.length()-1;
    
            int rulesLen = rules.length;
            boolean bingo = true;
    
            if(rulesLen == 1){
                // 只有一段(无*) 精准匹配
                if(!exactMatch(rules[0], target)){
                    bingo = false;
                }
            }else{
                for(int i=0; i<rulesLen; i++){
                    if(i == 0){
                        // 匹配第一段
                        if(!"".equals(rules[i])){
                            if(!firstMatch(rules[i], target)){
                                bingo = false;
                                break;
                            }
                        }
                    }else if(i == rulesLen-1){
                        // 匹配最后一段
                        if(!"".equals(rules[i])){
                            if(!lastMatch(rules[i], target)){
                                bingo = false;
                                break;
                            }
                        }
                    }else{
                        // 中间包含匹配(*rules[i]*)
                        if(!containMatch(rules[i], target)){
                            bingo = false;
                            break;
                        }
                    }
                }
            }
    
            if(bingo){
                System.out.println("true");
            }else{
                System.out.println("false");
            }
        }
    
        private static boolean exactMatch(String rule, String target){
            int len = rule.length();
    
            for(int i=0; i<len; i++){
                char ruleChar = rule.charAt(i);
                char targetChar;
                if(indexL < targetLen){
                    targetChar = target.charAt(indexL);
                }else{
                    return false;
                }
    
                if(ruleChar == '?'){
                    if(Character.isLetter(targetChar) || Character.isDigit(targetChar)){
                        indexL++;
                    }else{
                        break;
                    }
                }else{
                    if(ruleChar == targetChar){
                        indexL++;
                    }else{
                        return false;
                    }
                }
            }
    
            if(indexL != targetLen){
                return false;
            }
    
            return true;
        }
    
        private static boolean lastMatch(String rule, String target){
            int len = rule.length();
    
            for(int i=len-1; i>=0; i--){
                char ruleChar = rule.charAt(i);
                char targetChar;
                if(indexL <= indexR){
                    targetChar = target.charAt(indexR);
                }else{
                    return false;
                }
    
                if(ruleChar == '?'){
                    if(Character.isLetter(targetChar) || Character.isDigit(targetChar)){
                        indexR--;
                    }else{
                        break;
                    }
                }else{
                    if(ruleChar == targetChar){
                        indexR--;
                    }else{
                        return false;
                    }
                }
            }
    
            return true;
        }
    
        private static boolean firstMatch(String rule, String target){
            int len = rule.length();
    
            for(int i=0; i<len; i++){
                char ruleChar = rule.charAt(i);
                char targetChar;
                if(indexL < targetLen){
                    targetChar = target.charAt(indexL);
                }else{
                    return false;
                }
    
                if(ruleChar == '?'){
                    if(Character.isLetter(targetChar) || Character.isDigit(targetChar)){
                        indexL++;
                    }else{
                        break;
                    }
                }else{
                    if(ruleChar == targetChar){
                        indexL++;
                    }else{
                        return false;
                    }
                }
            }
    
            return true;
        }
    
        private static boolean containMatch(String rule, String target){
            int len = rule.length();
    
            boolean match = false;
            for(int i=indexL; i+len<targetLen; i++){
                int matchLen = 0;
                for(int j=0; j<len; j++){
                    char ruleChar = rule.charAt(j);
                    char targetChar = target.charAt(i+j);
                    if(ruleChar == '?'){
                        // ? 匹配字母或数字
                        if(Character.isLetter(targetChar) || Character.isDigit(targetChar)){
                            matchLen++;
                        }else{
                            break;
                        }
                    }else{
    
                        if(ruleChar == targetChar){
                            matchLen++;
                        }else{
                            break;
                        }
                    }
                }
                if(matchLen == len){
                    match = true;
                    indexL = i+len;
                    break;
                }
            }
    
            if(match){
                return true;
            }else{
                return false;
            }
        }
    
    
        /**
         * 正则 regex
         * @param in
         */
        private static void solution3(Scanner in){
            String rule = in.nextLine().toLowerCase();
            String target = in.nextLine().toLowerCase();
            
            String regex = rule.replaceAll("\\*{2,}", "\\*");
            regex = regex.replaceAll("\\?", "[0-9a-z]{1}");
            regex = regex.replaceAll("\\*", "[0-9a-z]{0,}");
    
            System.out.println(target.matches(regex));
        }
    }

  

