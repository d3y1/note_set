# java-HJ29 字符串加解密


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        /**
         * mod
         * @param args
         */
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
            String needToEncrypt = in.next();
            String needToDecrypt = in.next();
            System.out.println(encrypt(needToEncrypt));
            System.out.println(decrypt(needToDecrypt));
        }
    
        public static String encrypt(String s) {
            char[] cs = s.toCharArray();
            //foreach拿到的不是元素本身，而是一个新变量，所以这里不能用foreach
            //除非新建一个StringBuilder
            for(int i=0;i<s.length();i++) {
                if(cs[i]>='a' && cs[i]<='z') {
                    cs[i] = (char) ((cs[i]-'a'+1)%26 + 'A');
                }else if(cs[i]>='A' && cs[i]<='Z') {
                    cs[i] = (char) ((cs[i]-'A'+1)%26 + 'a');
                }else if(cs[i]>='0' && cs[i]<='9') {
                    cs[i] = (char) ((cs[i]-'0'+1)%10 + '0');
                    //0-9是10个数，不是9个！
                }
            }
            return String.valueOf(cs);
        }
    
        public static String decrypt(String s) {
            char[] cs = s.toCharArray();
            //foreach拿到的不是元素本身，而是一个新变量，所以这里不能用foreach
            //除非新建一个StringBuilder
            //注意减法要再加一个26或10，才可以正常循环起来
            for(int i=0;i<s.length();i++) {
                if(cs[i]>='a' && cs[i]<='z') {
                    cs[i] = (char) ((cs[i]-'a'-1+26)%26 + 'A');
                }else if(cs[i]>='A' && cs[i]<='Z') {
                    cs[i] = (char) ((cs[i]-'A'-1+26)%26 + 'a');
                }else if(cs[i]>='0' && cs[i]<='9') {
                    cs[i] = (char) ((cs[i]-'0'-1+10)%10 + '0');
                }
            }
            return String.valueOf(cs);
        }
    
    
    
    //    /**
    //     * Character
    //     * @param args
    //     */
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        while (in.hasNext()){
    //            String originStr = in.nextLine();
    //            String encryptStr = in.nextLine();
    //
    //            char[] originChars = originStr.toCharArray();
    //            char[] encryptChars = encryptStr.toCharArray();
    //
    //            StringBuilder enc = new StringBuilder();
    //            for(char aChar: originChars){
    //                if(Character.isLetter(aChar)){
    //                    if(Character.isLowerCase(aChar)){
    //                        if(aChar=='z'){
    //                            enc.append(Character.toUpperCase((char) (aChar-25)));
    //                        }else{
    //                            enc.append(Character.toUpperCase((char ) (aChar+1)));
    //                        }
    //                    }
    //                    if(Character.isUpperCase(aChar)){
    //                        if(aChar=='Z'){
    //                            enc.append(Character.toLowerCase((char) (aChar-25)));
    //                        }else{
    //                            enc.append(Character.toLowerCase((char ) (aChar+1)));
    //                        }
    //                    }
    //                }else if(Character.isDigit(aChar)){
    //                    if(aChar=='9'){
    //                        enc.append('0');
    //                    }else{
    //                        enc.append((char ) ((int) aChar +1));
    //                    }
    //                }else{
    //                    enc.append(aChar);
    //                }
    //
    //            }
    //            System.out.println(enc);
    //
    //            StringBuilder dec = new StringBuilder();
    //            for(char aChar: encryptChars){
    //                if(Character.isLetter(aChar)){
    //                    if(Character.isLowerCase(aChar)){
    //                        if(aChar=='a'){
    //                            dec.append(Character.toUpperCase((char) (aChar+25)));
    //                        }else{
    //                            dec.append(Character.toUpperCase((char ) (aChar-1)));
    //                        }
    //                    }
    //                    if(Character.isUpperCase(aChar)){
    //                        if(aChar=='A'){
    //                            dec.append(Character.toLowerCase((char) (aChar+25)));
    //                        }else{
    //                            dec.append(Character.toLowerCase((char ) (aChar-1)));
    //                        }
    //                    }
    //                }else if(Character.isDigit(aChar)){
    //                    if(aChar=='0'){
    //                        dec.append('9');
    //                    }else{
    //                        dec.append((char ) ((int) aChar -1));
    //                    }
    //                }else{
    //                    dec.append(aChar);
    //                }
    //            }
    //            System.out.println(dec);
    //        }
    //    }
    }

  

