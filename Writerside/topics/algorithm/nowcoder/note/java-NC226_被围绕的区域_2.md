# java-NC226 被围绕的区域_2

```java
import java.util.*;

/**
 * NC226 被围绕的区域
 * @author d3y1
 */
public class Solution {
    private int[] dx = new int[]{0, 1, 0, -1};
    private int[] dy = new int[]{1, 0, -1, 0};
    private int ROW;
    private int COL;
    private boolean[][] isVisited;

    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 程序入口
     *
     * @param board char字符型二维数组
     * @return char字符型二维数组
     */
    public char[][] surroundedArea (char[][] board) {
        // return solution3(board);
        return solution4(board);
    }

    /**
     * 模拟法: 边界bfs(由外向内)
     * @param board
     * @return
     */
    private char[][] solution3(char[][] board){
        ROW = board.length;
        COL = board[0].length;

        Queue<int[]> queue = new LinkedList<>();

        // 左右边界
        for(int i=0; i<ROW; i++){
            if(board[i][0] == 'O'){
                queue.offer(new int[]{i,0});
                board[i][0] = 'N';
            }
            if(board[i][COL-1] == 'O'){
                queue.offer(new int[]{i,COL-1});
                board[i][COL-1] = 'N';
            }
        }

        // 上下边界
        for(int j=0; j<COL; j++){
            if(board[0][j] == 'O'){
                queue.offer(new int[]{0,j});
                board[0][j] = 'N';
            }
            if(board[ROW-1][j] == 'O'){
                queue.offer(new int[]{ROW-1,j});
                board[ROW-1][j] = 'N';
            }
        }

        int[] cur;
        int x,y,nx,ny;
        while(!queue.isEmpty()){
            cur = queue.poll();
            x = cur[0];
            y = cur[1];
            for(int i=0; i<4; i++){
                nx = x+dx[i];
                ny = y+dy[i];
                if(isValid(nx,ny) && board[nx][ny]=='O'){
                    queue.offer(new int[]{nx, ny});
                    board[nx][ny] = 'N';
                }
            }
        }

        // O -> X and N -> O
        for(int i=0; i<ROW; i++){
            for(int j=0; j<COL; j++){
                // 剩下来的O 必被X围绕 -> 标记为X
                if(board[i][j] == 'O'){
                    board[i][j] = 'X';
                }
                // 新标记的N 未被X围绕 -> 还原为O
                else if(board[i][j] == 'N'){
                    board[i][j] = 'O';
                }
            }
        }

        return board;
    }

    /**
     * 是否合法(是否越界)
     * @param x
     * @param y
     * @return
     */
    private boolean isValid(int x, int y){
        if(x<0 || x>=ROW || y<0 || y>=COL){
            return false;
        }

        return true;
    }

    /**
     * 模拟法: 并查集
     * @param board
     * @return
     */
    private char[][] solution4(char[][] board){
        ROW = board.length;
        COL = board[0].length;

        // 边界O的父节点都是虚拟节点root
        UnionFind uf = new UnionFind(ROW*COL+1);
        int root = ROW*COL;

        for(int i=0; i<ROW; i++){
            for(int j = 0; j < COL; j++){
                // 遇到O 进行并查集合并
                if(board[i][j] == 'O'){
                    // 边界O 与 虚拟节点root 合并成一个连通区域
                    if(i==0 || i==ROW-1 || j==0 || j==COL-1){
                        uf.union(loc(i, j), root);
                    }
                    // 非边界 与上下左右合并成一个连通区域
                    else{
                        // up
                        if(i>0 && board[i-1][j]=='O'){
                            uf.union(loc(i, j), loc(i-1, j));
                        }
                        // down
                        if(i<ROW-1 && board[i+1][j]=='O'){
                            uf.union(loc(i, j), loc(i+1, j));
                        }
                        // left
                        if(j>0 && board[i][j-1]=='O'){
                            uf.union(loc(i, j), loc(i, j-1));
                        }
                        // right
                        if(j<COL-1 && board[i][j+1] =='O'){
                            uf.union(loc(i, j), loc(i, j+1));
                        }
                    }
                }
            }
        }

        for(int i=0; i<ROW; i++){
            for(int j=0; j<COL; j++){
                // 与虚拟节点root 在一个连通区域 -> 未被X围绕
                if(uf.isConnected(loc(i, j), root)){
                    board[i][j] = 'O';
                }
                // 与虚拟节点root 不在在一个连通区域 -> 可被X围绕
                else{
                    board[i][j] = 'X';
                }
            }
        }

        return board;
    }

    /**
     * 坐标位置: 二维转一维(等价于一个结点)
     * @param i
     * @param j
     * @return
     */
    private int loc(int i, int j){
        return i*COL+j;
    }

    /**
     * 并查集类
     */
    private class UnionFind{
        // 连通分量
        int connect;
        // 记录父节点
        int[] parent;

        // 构造函数 n为结点个数
        UnionFind(int n){
            // 初始连通分量
            this.connect = n;
            this.parent = new int[n];
            for(int i=0; i<n; i++){
                // 初始父节点指向自己
                parent[i]=i;
            }
        }

        // 找到x的根节点
        int find(int x){
            while(parent[x] != x){
                // 显著提高效率(减少搜索深度 更快找到根节点)
                parent[x] = parent[parent[x]];
                x = parent[x];
            }
            return x;
        }

        // 连通p和q
        void union(int p, int q){
            int rootP = find(p);
            int rootQ = find(q);
            if(rootP != rootQ){
                parent[rootP] = rootQ;
                connect--;
            }
        }

        // 返回连通分量
        int connect(){
            return connect;
        }

        // 是否连通
        boolean isConnected(int p, int q) {
            return find(p) == find(q);
        }
    }
}
```
