# java-NC199 字符串解码

```java
import java.util.*;

/**
 * NC199 字符串解码
 * @author d3y1
 */
public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 类似 -> HJ50 四则运算
     *
     * @param s string字符串
     * @return string字符串
     */
    public String decodeString (String s) {
        // return solution1(s);
        // return solution11(s);
        return solution111(s);
        // return solution2(s);
    }

    /**
     * 递归
     * @param s
     * @return
     */
    private String solution1(String s){
        int len = s.length();
        StringBuilder result = new StringBuilder();
        char ch;
        int num = 0;
        String part;
        for(int i=0; i<len; i++){
            ch = s.charAt(i);
            // digit
            if(Character.isDigit(ch)){
                num = num*10+(ch-'0');
            }
            // [
            else if(ch == '['){
                int cnt = 1;
                char next;
                int j;
                for(j=i+1; j<len; j++){
                    next = s.charAt(j);
                    if(next == '['){
                        cnt++;
                    }
                    if(next == ']'){
                        cnt--;
                    }
                    if(cnt == 0){
                        break;
                    }
                }
                part = decodeString(s.substring(i+1, j));
                while(num > 0){
                    result.append(part);
                    num--;
                }
                i = j;
            }
            // letter
            else if(Character.isLetter(ch)){
                result.append(ch);
            }
        }

        return result.toString();
    }

    /**
     * 递归
     * @param s
     * @return
     */
    private String solution11(String s){
        int n = s.length();
        StringBuilder result = new StringBuilder();
        char ch;
        int k = 0;
        String c;
        for(int i=0; i<n; i++){
            ch = s.charAt(i);
            // digit
            if(Character.isDigit(ch)){
                k = k*10+(ch-'0');
            }
            // [
            else if(ch == '['){
                int cnt = 1;
                char next;
                int j;
                for(j=i+1; j<n; j++){
                    next = s.charAt(j);
                    if(next == '['){
                        cnt++;
                    }
                    if(next == ']'){
                        cnt--;
                    }
                    if(cnt == 0){
                        break;
                    }
                }
                c = decodeString(s.substring(i+1, j));
                while(k > 0){
                    result.append(c);
                    k--;
                }
                i = j;
            }
            // letter
            else if(Character.isLetter(ch)){
                result.append(ch);
            }
        }

        return result.toString();
    }

    /**
     * 递归
     * @param s
     * @return
     */
    private String solution111(String s){
        int n = s.length();

        StringBuilder sb = new StringBuilder();

        int k;
        char ch;
        for(int i=0; i<n; i++){
            k = 0;
            ch = s.charAt(i);

            // k[c]
            if(Character.isDigit(ch)){
                // k
                while(Character.isDigit(ch)){
                    k = k*10+(ch-'0');
                    ch = s.charAt(++i);
                }
                // c
                String c = "";
                if(ch == '['){
                    int cnt = 1;
                    int j = i+1;
                    while(j < n){
                        if(s.charAt(j) == '['){
                            cnt++;
                        }
                        if(s.charAt(j) == ']'){
                            cnt--;
                        }
                        if(cnt == 0){
                            c = decodeString(s.substring(i+1, j));
                            break;
                        }
                        j++;
                    }
                    i = j;
                }
                // c重复k次
                while(k-- > 0){
                    sb.append(c);
                }
            }

            // c
            else if(Character.isLetter(ch)){
                sb.append(ch);
            }
        }

        return sb.toString();
    }

    /**
     * 迭代: 栈
     * @param s
     * @return
     */
    private String solution2(String s){
        Stack<Integer> numStack = new Stack<>();
        Stack<String> resStack = new Stack<>();
        StringBuilder result = new StringBuilder();

        int len = s.length();
        char ch;
        int num = 0;
        for(int i=0; i<len; i++){
            ch = s.charAt(i);
            // digit
            if(Character.isDigit(ch)){
                num = num*10 + (ch-'0');
            }
            // [
            else if(ch == '['){
                numStack.push(num);
                num = 0;
                resStack.push(result.toString());
                result = new StringBuilder();
            }
            // letter
            else if(Character.isLetter(ch)){
                result.append(ch);
            }
            // ]
            else if(ch == ']'){
                int times = numStack.pop();
                StringBuilder part = new StringBuilder(resStack.pop());
                for(int j=1; j<=times; j++){
                    part.append(result);
                }
                result = part;
            }
        }

        return result.toString();
    }
}
```
