# java-NC379 重排字符串


    import java.util.*;
    
    /**
     * NC379 重排字符串
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 顺便试试 堆的各种排序写法(大根堆)
         * 
         * @param str string字符串
         * @return string字符串
         */
        public String rearrangestring (String str) {
            // return solution1(str);
            return solution2(str);
        }
    
        /**
         * 贪心+最大堆(优先队列)
         * @param str
         * @return
         */
        private String solution1(String str){
            int len = str.length();
            int[] charCount = new int[26];
            PriorityQueue<Letter> maxHeap = new PriorityQueue<>((o1, o2)->(o2.cnt-o1.cnt));
    
            // 统计字符次数
            for(int i=0; i<len; i++){
                charCount[str.charAt(i)-'a']++;
            }
    
            // build maxHeap
            for(int i=0; i<26; i++){
                if(charCount[i] > 0){
                    maxHeap.add(new Letter((char)('a'+i), charCount[i]));
                }
            }
    
            // 贪心: 最多字符+次多字符
            StringBuilder sb = new StringBuilder();
            Letter first,second;
            while(maxHeap.size() >= 2){
                first = maxHeap.poll();
                second = maxHeap.poll();
                sb.append(first.letter);
                sb.append(second.letter);
                if(first.cnt > 1){
                    first.cnt--;
                    maxHeap.add(first);
                }
                if(second.cnt > 1){
                    second.cnt--;
                    maxHeap.add(second);
                }
            }
    
            if(!maxHeap.isEmpty()){
                first = maxHeap.poll();
                if(first.cnt > 1){
                    return "";
                }else{
                    sb.append(first.letter);
                }
            }
    
            return sb.toString();
        }
    
        ///////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 贪心+最大堆(优先队列)
         * @param str
         * @return
         */
        private String solution2(String str){
            System.out.println(str);
            int n = str.length();
    
            // 统计字母次数
            int[] cnt = new int[26];
            for(char ch: str.toCharArray()){
                cnt[ch-'a']++;
            }
    
            // 最大堆
            // PriorityQueue<Letter> maxHeap = new PriorityQueue<>(new Comparator<Letter>(){
            //     @Override
            //     public int compare(Letter o1, Letter o2){
            //         // cnt 降序
            //         if(o1.cnt != o2.cnt){
            //             return o2.cnt-o1.cnt;
            //         }
            //         // letter 升序
            //         else{
            //             return o1.letter-o2.letter;
            //         }
            //     }
            // });
            // PriorityQueue<Letter> maxHeap = new PriorityQueue<>((o1, o2) -> {
            //     // cnt 降序
            //     if(o1.cnt != o2.cnt){
            //         return o2.cnt-o1.cnt;
            //     }
            //     // letter 升序
            //     else{
            //         return o1.letter-o2.letter;
            //     }
            // });
            // PriorityQueue<Letter> maxHeap = new PriorityQueue<>(new Comparator<Letter>(){
            //     @Override
            //     public int compare(Letter o1, Letter o2){
            //         // cnt 降序
            //         return o2.cnt-o1.cnt;
            //     }
            // });
            PriorityQueue<Letter> maxHeap = new PriorityQueue<>((o1, o2) -> (o2.cnt-o1.cnt));
            // PriorityQueue<Letter> maxHeap = new PriorityQueue<>(Comparator.comparing(o -> o.cnt, Comparator.reverseOrder()));
            // PriorityQueue<Letter> maxHeap = new PriorityQueue<>(Comparator.comparing(Letter::getCnt, Comparator.reverseOrder()));
            // PriorityQueue<Letter> maxHeap = new PriorityQueue<>(Comparator.comparingInt(Letter::getCnt).reversed());
    
            // 入堆
            for(int i=0; i<26; i++){
                if(cnt[i] > 0){
                    maxHeap.offer(new Letter((char)(i+'a'), cnt[i]));
                }
            }
    
            StringBuilder result = new StringBuilder();
            // 测试用例: aaaaabbbccdd aabbccddee
            Letter top1,top2;
            // 贪心
            while(maxHeap.size() >= 2){
                top1 = maxHeap.poll();
                top2 = maxHeap.poll();
                result.append(top1.letter);
                result.append(top2.letter);
                top1.cnt--;
                top2.cnt--;
                if(top1.cnt > 0){
                    maxHeap.offer(top1);
                }
                if(top2.cnt > 0){
                    maxHeap.offer(top2);
                }
            }
    
            if(maxHeap.size() == 1){
                if(maxHeap.peek().cnt == 1){
                    result.append(maxHeap.poll().letter);
                }else{
                    return "";
                }
            }
    
            return result.toString();
        }
    
        /**
         * 英文字母类
         */
        private class Letter {
            // 小写英文字母
            private char letter;
            // 统计字母次数
            private int cnt;
    
            private Letter(char letter, int cnt){
                this.letter = letter;
                this.cnt = cnt;
            }
    
            private int getCnt(){
                return cnt;
            }
        }
    }

  

