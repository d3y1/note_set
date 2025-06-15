# java-ZJ5 编程题1(推箱子)


    import java.util.LinkedList;
    import java.util.Queue;
    import java.util.Scanner;
    
    public class Main {
        private static final int[] dX = new int[]{0, 0, 1, -1};
        private static final int[] dY = new int[]{1, -1, 0, 0};
    
        private static int row;
        private static int column;
        private static char[][] board;
        private static boolean[][][][] visited;
        private static Location start;
        private static Location end;
        private static Location startBox;
        private static int result = Integer.MAX_VALUE;
    
        private static Queue<Step> stepsQueue = new LinkedList<>();
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                row = in.nextInt();
                column = in.nextInt();
                board = new char[row][column];
                for(int i=0; i<row; i++){
                    board[i] = in.next().toCharArray();
                }
    
                visited = new boolean[row][column][row][column];
    
                for(int i=0; i<row; i++){
                    for(int j=0; j<column; j++){
                        if(board[i][j] == 'S'){
                            start = new Location(i, j);
                        }
                        if(board[i][j] == 'E'){
                            end = new Location(i, j);
                        }
                        if(board[i][j] == '0'){
                            startBox = new Location(i, j);
                        }
                    }
                }
    
                solutionBFS();
            }
        }
        
        /**
         * 模拟法: 适合BFS
         */
        private static void solutionBFS(){
            Step startStep = new Step(start.x, start.y, startBox.x, startBox.y, 0);
            stepsQueue.add(startStep);
    
            bfs();
    
            if(result == Integer.MAX_VALUE){
                System.out.println(-1);
            }else{
                System.out.println(result);
            }
        }
    
        /**
         * BFS
         */
        private static void bfs(){
            while (!stepsQueue.isEmpty()){
                Step curr = stepsQueue.poll();
                if(curr.bx==end.x && curr.by==end.y){
                    result = curr.count;
                    break;
                }
                for(int i=0; i<4; i++){
                    Step next;
                    // 下一步 到达 箱子位置
                    if(curr.px+dX[i]==curr.bx && curr.py+dY[i]==curr.by){
                        // 人和箱子都移动
                        next = new Step(curr.px + dX[i], curr.py + dY[i], curr.bx + dX[i], curr.by + dY[i], curr.count + 1);
                    }else{
                        // 仅人移动
                        next = new Step(curr.px + dX[i], curr.py + dY[i], curr.bx, curr.by, curr.count + 1);
                    }
                    if(canGo(next)){
                        visited[next.px][next.py][next.bx][next.by] = true;
                        stepsQueue.add(next);
                    }
                }
            }
        }
        
        /**
         * 下一步是否可行
         * @param next
         * @return
         */
        private static boolean canGo(Step next){
            // 验证人位置
            // 越界
            if(next.px<0 || next.py<0 || next.px>=row || next.py>=column){
                return false;
            }
            // 墙壁
            if(board[next.px][next.py] == '#'){
                return false;
            }
            
            // 验证箱子位置
            // 越界
            if(next.bx<0 || next.by<0 || next.bx>=row || next.by>=column){
                return false;
            }
            // 墙壁
            if(board[next.bx][next.by] == '#'){
                return false;
            }
    
            // 已访问
            if(visited[next.px][next.py][next.bx][next.by]){
                return false;
            }
    
            return true;
        }
    
        /**
         * 位置(row, column)
         */
        private static class Location {
            int x;
            int y;
    
            private Location(int x, int y){
                this.x = x;
                this.y = y;
            }
        }
    
        /**
         * 移动: 步
         */
        private static class Step {
            // 人位置
            int px;
            int py;
    
            // 箱子位置
            int bx;
            int by;
    
            int count;
    
            private Step(int px, int py, int bx, int by, int count){
                this.px = px;
                this.py = py;
                this.bx = bx;
                this.by = by;
                this.count = count;
            }
        }
    }

  

