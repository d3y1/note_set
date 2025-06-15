# java-HJ63 DNA序列


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args) {
            Scanner in =  new Scanner(System.in);
    
            while (in.hasNext()){
                String dna = in.nextLine();
                int subLen = in.nextInt();
    
                solution(dna, subLen);
            }
        }
    
        /**
         * 滑动窗口 正则表达式
         * @param dna
         * @param subLen
         */
        private static void solution(String dna, int subLen){
    
            int gcCount = 0;
            String result = "";
            for(int i=0; i+subLen<=dna.length(); i++){
                String subStr = dna.substring(i, i+subLen);
                String replacedSubStr = subStr.replaceAll("[GC]","");
    
                int tmpGcCount = subLen-replacedSubStr.length();
                if(tmpGcCount > gcCount){
                    gcCount = tmpGcCount;
                    result = subStr;
                }
            }
    
            System.out.println(result);
        }
    }

  

