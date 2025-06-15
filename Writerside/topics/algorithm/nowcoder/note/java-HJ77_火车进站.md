# java-HJ77 火车进站


    import java.util.ArrayList;
    import java.util.Collections;
    import java.util.Scanner;
    import java.util.Stack;
    
    public class Main {
        private static ArrayList<String> result = new ArrayList<>();
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 栈
         * @param in
         */
        private static void solution(Scanner in){
            int num = in.nextInt();
            int[] trains = new int[num];
    
            // 列车编号
            for(int i=0; i<num; i++){
                trains[i] = in.nextInt();
            }
    
            result = new ArrayList<>();
    
            // 火车站
            Stack<Integer> station = new Stack<>();
    
            // 发车
            depart(trains, station, 0, 0, "");
    
            Collections.sort(result);
    
            for(String seq: result){
                System.out.println(seq);
            }
        }
    
        /**
         * 递归
         * @param trains    列车初始编号序列
         * @param station   火车站
         * @param inNum     驶入火车站列车数
         * @param outNum    驶出火车站列车数
         * @param seqStr    驶出火车站列车序列
         */
        private static void depart(int[] trains, Stack<Integer> station, int inNum, int outNum, String seqStr){
            // 列车全部驶出
            if(outNum == trains.length){
                result.add(seqStr);
                return;
            }
    
            if(!station.isEmpty()){
                // 驶出
                Integer seq = station.pop();
                depart(trains, station, inNum, outNum+1, seqStr+seq+" ");
                // 恢复
                station.push(seq);
            }
    
            if(inNum < trains.length){
                // 驶入
                station.push(trains[inNum]);
                depart(trains, station, inNum+1, outNum, seqStr);
                // 恢复
                station.pop();
            }
        }
    }

  

