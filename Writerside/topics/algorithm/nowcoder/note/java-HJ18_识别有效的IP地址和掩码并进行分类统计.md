# java-HJ18 识别有效的IP地址和掩码并进行分类统计


    import java.util.Scanner;
    
    public class Main {
        private static int aNum = 0;
        private static int bNum = 0;
        private static int cNum = 0;
        private static int dNum = 0;
        private static int eNum = 0;
        private static int errNum = 0;
        private static int pNum = 0;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                String line = in.nextLine();
    
                String[] ipMask = line.split("~");
                int ipFirst = getIpSeg(ipMask[0], 0);
    
                if(ipFirst==0 || ipFirst==127){
                    continue;
                }
                if(maskInvalid(ipMask[1])){
                    errNum++;
                    continue;
                }
                if(ipInvalid(ipMask[0])){
                    errNum++;
                    continue;
                }
                if(1<=ipFirst && ipFirst<=126){
                    aNum++;
                }
                if(128<=ipFirst && ipFirst<=191){
                    bNum++;
                }
                if(192<=ipFirst && ipFirst<=223){
                    cNum++;
                }
                if(224<=ipFirst && ipFirst<=239){
                    dNum++;
                }
                if(240<=ipFirst && ipFirst<=255){
                    eNum++;
                }
                int ipSecond = getIpSeg(ipMask[0], 1);
                if(ipFirst==10 || (ipFirst==172 && (16<=ipSecond && ipSecond<=31)) || (ipFirst==192 && ipSecond==168)){
                    pNum++;
                }
            }
    
            System.out.println(aNum + " " + bNum + " " + cNum + " " + dNum + " " + eNum + " " + errNum + " " + pNum);
        }
    
        public static boolean maskInvalid(String mask){
            String[] maskArray = mask.split("\\.");
    
            if(maskArray.length != 4){
                return true;
            }
            String maskBinary = toBinary(maskArray[0]) + toBinary(maskArray[1]) + toBinary(maskArray[2]) + toBinary(maskArray[3]);
            if(!maskBinary.matches("[1]{1,}[0]{1,}")){
                return true;
            }
    
            return false;
        }
    
        public static String toBinary(String num){
            StringBuilder numBinary = new StringBuilder(Integer.toBinaryString(Integer.parseInt(num)));
            while(numBinary.length() < 8){
                numBinary.insert(0, "0");
            }
    
            return numBinary.toString();
        }
    
        public static boolean ipInvalid(String ip){
            String[] ipArray = ip.split("\\.");
    
            if(ipArray.length != 4){
                return true;
            }
            if(Integer.parseInt(ipArray[0])>255 || Integer.parseInt(ipArray[1])>255 || Integer.parseInt(ipArray[2])>255 || Integer.parseInt(ipArray[3])>255){
                return true;
            }
    
            return false;
        }
    
        public static int getIpSeg(String ip, int seg){
            String[] ipArray = ip.split("\\.");
    
            return Integer.parseInt(ipArray[seg]);
        }
    }

  

