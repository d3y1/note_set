# java-HJ67 24点游戏算法


    import java.util.HashSet;
    import java.util.Scanner;
    import javax.script.ScriptEngine;
    import javax.script.ScriptEngineManager;
    import javax.script.ScriptException;
    
    public class Main {
        private static HashSet<String> numsCombineSet = new HashSet<>();
        private static boolean can24 = false;
        private static boolean[] visited = new boolean[4];
    
        private static final String[] ops = new String[]{"+", "-", "*", "/"};
    
        public static void main(String[] args) throws ScriptException {
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                int[] nums = new int[]{in.nextInt(), in.nextInt(), in.nextInt(), in.nextInt()};
    
                numsCombineSet = new HashSet<>();
                can24 = false;
                visited = new boolean[4];
    
                solution(nums);
                solutionDFS(nums);
            }
        }
    
        /**
         * dfs
         * @param nums
         */
        private static void solutionDFS(int[] nums){
    
            dfs(nums, 0, 0d);
    
            if(can24){
                System.out.println("true");
            }else{
                System.out.println("false");
            }
        }
    
        private static boolean dfs(int[] nums, int opTimes, double result){
            if(opTimes==4 && result==24d){
                can24 = true;
                return true;
            }
    
            for(int i=0; i<4; i++){
                if(!visited[i]){
                    visited[i] = true;
    
                    if(opTimes == 0){
                        if(dfs(nums, opTimes+1, result+nums[i])){
                            return true;
                        }
                    }else{
                        if(dfs(nums, opTimes+1, result+nums[i])
                                || dfs(nums, opTimes+1, result-nums[i])
                                || dfs(nums, opTimes+1, result*nums[i])
                                || dfs(nums, opTimes+1, result/nums[i])){
                            return true;
                        }
                    }
    
                    visited[i] = false;
                }
            }
    
            return false;
        }
    
    
        /**
         * 递归
         * @param nums
         * @throws ScriptException
         */
        private static void solution(int[] nums) throws ScriptException {
            // 生成各种数字组合
            numsCombine(nums, 0);
    
            for(String numsSeq: numsCombineSet){
                if(is24(numsSeq)){
                    break;
                }
            }
    
            if(can24){
                System.out.println("true");
            }else{
                System.out.println("false");
            }
        }
    
        private static void numsCombine(int[] nums, int i) {
    
            StringBuilder sb = new StringBuilder();
            sb.append(nums[0]);
            for(int j=1; j<=3; j++){
                sb.append(",");
                sb.append(nums[j]);
            }
            numsCombineSet.add(sb.toString());
    
            for(int j=i; j<=3; j++){
                swap(nums, i, j);
                numsCombine(nums, i+1);
                swap(nums, i, j);
            }
        }
    
        private static boolean is24(String nums) throws ScriptException {
            String[] numsArray = nums.split(",");
    
            String opStr = numsArray[0];
            if(operate(numsArray, opStr, 1)){
                return true;
            }
    
            return false;
        }
    
        private static boolean operate(String[] nums, String opStr, int opTimes) throws ScriptException {
            if(opTimes == 4){
                ScriptEngine scriptEngine = new ScriptEngineManager().getEngineByName("nashorn");
                if("24".equals(String.valueOf(scriptEngine.eval(opStr)))){
                    // 打印值为24的表达式
                    System.out.println(opStr);
                    can24 = true;
                    return true;
                };
            }
    
            if(opTimes <= 3){
                for(int i=0; i<=3; i++){
                    String tmpOpStr = "("+opStr+ops[i]+nums[opTimes]+")";
                    opTimes++;
                    if(operate(nums, tmpOpStr, opTimes)){
                        return true;
                    }
                    opTimes--;
                }
            }
    
            return false;
        }
    
        private static void swap(int[] nums, int i, int j){
            int tmp = nums[i];
            nums[i] = nums[j];
            nums[j] = tmp;
        }
    }

  

