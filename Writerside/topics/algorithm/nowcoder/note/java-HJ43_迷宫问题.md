# java-HJ43 迷宫问题


    import java.util.LinkedList;
    import java.util.Queue;
    import java.util.Scanner;
    
    /**
     * HJ43 迷宫问题
     * @author d3y1
     */
    public class Main {
        public static void main(String[] args) {
            // solution1();
            // solution2();
            solution3();
        }
    
        private static int[] dX = new int[]{0, 0, 1, -1};
        private static int[] dY = new int[]{1, -1, 0, 0};
    
        private static int row;
        private static int col;
        private static int[][] matrix;
        private static boolean[][] visited;
        private static Step[][] pre;
    
        private static Queue<Step> stepsQueue = new LinkedList<>();
    
        /**
         * dfs
         */
        private static void solution1(){
            Scanner in = new Scanner(System.in);
            
            row = in.nextInt();
            col = in.nextInt();
    
            matrix = new int[row][col];
            visited = new boolean[row][col];
            pre = new Step[row][col];
            for(int i=0; i<row; i++){
                for(int j=0; j<col; j++){
                    matrix[i][j] = in.nextInt();
                }
            }
    
            Step start = new Step(0, 0);
    
            dfs(start);
    
            printPath(row-1, col-1);
        }
    
        private static void dfs(Step curr){
            if(curr.x==row-1 && curr.y==col-1){
                return;
            }
    
            visited[curr.x][curr.y] = true;
    
            for(int i=0; i<4; i++){
                Step next = new Step(curr.x+dX[i], curr.y+dY[i]);
                if(canGo(next)){
                    pre[next.x][next.y] = curr;
                    dfs(next);
                }
            }
            visited[curr.x][curr.y] = false;
        }
    
    
        /**
         * bfs
         */
        private static void solution2(){
            Scanner in = new Scanner(System.in);
    
            row = in.nextInt();
            col = in.nextInt();
    
            matrix = new int[row][col];
            visited = new boolean[row][col];
            pre = new Step[row][col];
            for(int i=0; i<row; i++){
                for(int j=0; j<col; j++){
                    matrix[i][j] = in.nextInt();
                }
            }
    
            Step start = new Step(0, 0);
            stepsQueue.add(start);
    
            bfs();
    
            printPath(row-1, col-1);
        }
    
        private static void bfs(){
            while (stepsQueue.size()!=0){
                Step curr = stepsQueue.poll();
                if(curr.x==row-1 && curr.y==col-1){
                    break;
                }
                for(int i=0; i<4; i++){
                    Step next = new Step(curr.x+dX[i], curr.y+dY[i]);
                    if(canGo(next)){
                        stepsQueue.add(next);
                        pre[next.x][next.y] = curr;
                    }
                }
                visited[curr.x][curr.y] = true;
            }
        }
    
        private static boolean canGo(Step next){
            // 越界
            if(next.x<0 || next.y<0 || next.x>=row || next.y>=col){
                return false;
            }
    
            // 墙壁
            if(matrix[next.x][next.y] == 1){
                return false;
            }
    
            // 已访问
            if(visited[next.x][next.y]){
                return false;
            }
    
            return true;
        }
    
        /**
         * 打印路径
         * @param x
         * @param y
         */
        private static void printPath(int x, int y){
            if(x==0 && y==0){
                System.out.println("("+x+","+y+")");
                return;
            }
    
            Step previous = pre[x][y];
            printPath(previous.x, previous.y);
    
            System.out.println("("+x+","+y+")");
        }
    
        private static class Step {
            int x;
            int y;
    
            private Step(int x, int y){
                this.x = x;
                this.y = y;
            }
        }
        
        /////////////////////////////////////////////////////////////////////////////////////
    
        private static int n,m;
        private static boolean[][] isVisited;
        private static int[] dx = new int[]{-1, 1, 0, 0};
        private static int[] dy = new int[]{0, 0, -1, 1};
    
        /**
         * bfs
         */
        private static void solution3(){
            Scanner in = new Scanner(System.in);
            n = in.nextInt();
            m = in.nextInt();
            isVisited = new boolean[n][m];
            int[][] maze = new int[n][m];
            for(int i=0; i<n; i++){
                for(int j=0; j<m; j++){
                    maze[i][j] = in.nextInt();
                }
            }
    
            Queue<Node> queue = new LinkedList<>();
            queue.offer(new Node(0, 0));
            isVisited[0][0] = true;
    
            int size;
            Node node,path=null;
            int nextRow,nextCol;
            boolean found = false;
            while(!queue.isEmpty()){
                if(found){
                    break;
                }
                size = queue.size();
                while(size-- > 0){
                    node = queue.poll();
                    if(node.row==n-1 && node.col==m-1){
                        found = true;
                        path = node;
                    }
                    if(found){
                        break;
                    }
                    for(int i=0; i<4; i++){
                        nextRow = node.row+dx[i];
                        nextCol = node.col+dy[i];
                        if(isValid(nextRow, nextCol) && !isVisited[nextRow][nextCol]){
                            isVisited[nextRow][nextCol] = true;
                            if(maze[nextRow][nextCol] == 0){
                                queue.offer(new Node(nextRow, nextCol, node));
                            }
                        }
                    }
                }
            }
    
            StringBuilder sb = new StringBuilder();
            while(path != null){
                sb.insert(0, "("+path.row+","+path.col+")"+"\n");
                path = path.pre;
            }
    
            System.out.println(sb);
        }
    
        private static boolean isValid(int row, int col){
            if(0<=row&&row<n && 0<=col&&col<m){
                return true;
            }
    
            return false;
        }
    
        private static class Node {
            int row;
            int col;
            public Node(int row, int col){
                this.row = row;
                this.col = col;
            }
    
            public Node(int row, int col, Node pre){
                this.row = row;
                this.col = col;
                this.pre = pre;
            }
    
            Node pre = null;
        }
    }

  

