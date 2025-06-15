# java-ZJ6 编程题2(房间的人重新分配)


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法
         * 
         * distribute -> room_i
         * 不论room_i的位置在哪里,其房间内再分配后的人数总是最少的.
         * 如果出现多个房间内人数都与最少人数相同的情况,那么从room_x向前推,第一个人数最少的房间即为room_i.
         * 
         * @param in
         */
        private static void solution(Scanner in){
            // 房间数量
            int total = in.nextInt();
            // 最后一个人被分配的房间号
            int lastIn = in.nextInt();
            // 每个房间人数, 从1开始
            long[] rooms = new long[total+1];
            // 房间的最少人数
            long pMin = Integer.MAX_VALUE;
    
            for(int i=1; i<=total; i++){
                rooms[i] = in.nextLong();
                pMin = Math.min(pMin, rooms[i]);
            }
    
            // 已重新分配的房间号,即: 房间号lastIn(包含lastIn)前面人数最少的房间号
            int distribute = lastIn;
            while(rooms[distribute] != pMin){
    //            distribute = (distribute>1) ? distribute-1 : total;
                distribute = (distribute-2+total)%total+1;
            }
    
            if(distribute < lastIn){
                for(int i=1; i<=total; i++){
                    if(i < distribute){
                        rooms[i] -= pMin;
                    }else if(i == distribute){
                        rooms[i] = pMin*total+(lastIn-distribute);
                    }else if(distribute<i && i<=lastIn){
                        rooms[i] -= (pMin+1);
                    }else{
                        rooms[i] -= pMin;
                    }
                }
            }
    
            if(distribute == lastIn){
                for(int i=1; i<=total; i++){
                    if(i != distribute){
                        rooms[i] -= pMin;
                    }else{
                        rooms[i] = pMin*total;
                    }
                }
            }
    
            if(distribute > lastIn){
                for(int i=1; i<=total; i++){
                    if(i <= lastIn){
                        rooms[i] -= (pMin+1);
                    }else if(lastIn<i && i<distribute){
                        rooms[i] -= pMin;
                    }else if(i == distribute){
                        rooms[i] = pMin*total+(lastIn)+(total-distribute);
                    }else{
                        rooms[i] -= (pMin+1);
                    }
                }
            }
    
            for(int i=1; i<=total; i++){
                System.out.print(rooms[i]+" ");
            }
        }
    }

  

