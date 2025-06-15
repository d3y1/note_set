# java-HJ39 判断两个IP是否属于同一子网


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                String mask = in.nextLine();
                String ip1 = in.nextLine();
                String ip2 = in.nextLine();
    
                if(maskInvalid(mask) || ipInvalid(ip1) || ipInvalid(ip2)){
                    System.out.println(1);
                }else{
                    if(isSubNet(mask, ip1, ip2)){
                        System.out.println(0);
                    }else{
                        System.out.println(2);
                    }
                }
            }
        }
    
        private static boolean maskInvalid(String mask){
            String[] maskArray = mask.split("\\.");
    
            if(maskArray.length != 4){
                return true;
            }
    
            for(String seg: maskArray){
                if(Integer.parseInt(seg)<0 || 255<Integer.parseInt(seg)){
                    return true;
                }
            }
    
            String maskBinary = toBinary(maskArray[0]) + toBinary(maskArray[1]) + toBinary(maskArray[2]) + toBinary(maskArray[3]);
            if(!maskBinary.matches("[1]{1,}[0]{1,}")){
                return true;
            }
    
            return false;
        }
    
        private static String toBinary(String num){
    
            return String.format("%08d", Integer.parseInt(Integer.toBinaryString(Integer.parseInt(num))));
        }
    
        private static boolean ipInvalid(String ip){
            String[] ipArray = ip.split("\\.");
    
            if(ipArray.length != 4){
                return true;
            }
    
            for(String seg: ipArray){
                if(Integer.parseInt(seg)<0 || 255<Integer.parseInt(seg)){
                    return true;
                }
            }
    
            return false;
        }
    
        private static boolean isSubNet(String mask, String ip1, String ip2){
            String[] maskArray = mask.split("\\.");
            String[] ip1Array = ip1.split("\\.");
            String[] ip2Array = ip2.split("\\.");
    
            for(int i=0; i<4; i++){
                if((Integer.parseInt(maskArray[i]) & Integer.parseInt(ip1Array[i])) != (Integer.parseInt(maskArray[i])&Integer.parseInt(ip2Array[i]))){
                    return false;
                }
            }
    
            return true;
        }
    }

  

