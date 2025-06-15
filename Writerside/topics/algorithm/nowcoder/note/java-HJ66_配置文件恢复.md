# java-HJ66 配置文件恢复


    import java.util.HashMap;
    import java.util.Scanner;
    
    public class Main {
        
        private static final HashMap<String, String> commandMap = new HashMap<>();
    
        static {
            commandMap.put("reset", "reset what");
            commandMap.put("reset board", "board fault");
            commandMap.put("board add", "where to add");
            commandMap.put("board delete", "no board at all");
            commandMap.put("reboot backplane", "impossible");
            commandMap.put("backplane abort", "install first");
        }
    
        public static void main(String[] args) {
            Scanner in =  new Scanner(System.in);
    
            while (in.hasNext()){
                String command = in.nextLine();
    
                solution(command);
            }
        }
    
        /**
         * map
         * @param command
         */
        private static void solution(String command){
            String[] subCommands = command.trim().split(" ");
            int matchCount = 0;
            String matchKey = "";
            if(subCommands.length == 1){
                for(String key: commandMap.keySet()){
                    String[] subKeys = key.trim().split(" ");
                    if(subKeys.length == 1){
                        if(subKeys[0].startsWith(subCommands[0])){
                            matchCount++;
                            matchKey = key;
                        }
                    }
                }
            }else if(subCommands.length == 2){
                for(String key: commandMap.keySet()){
                    String[] subKeys = key.trim().split(" ");
                    if(subKeys.length == 2){
                        if(subKeys[0].startsWith(subCommands[0]) && subKeys[1].startsWith(subCommands[1])){
                            matchCount++;
                            matchKey = key;
                        }
                    }
                }
            }
    
            if(matchCount == 1){
                System.out.println(commandMap.get(matchKey));
            }else{
                System.out.println("unknown command");
            }
        }
    }

  

