# java-HJ16 购物单


    import java.util.ArrayList;
    import java.util.Arrays;
    import java.util.Collections;
    import java.util.Comparator;
    import java.util.HashSet;
    import java.util.List;
    import java.util.Scanner;
    import java.util.Set;
    
    
    public class Main {
        /**
         * test case:
         * 1500 7
         * 500 1 0
         * 400 4 0
         * 300 5 1
         * 400 5 1
         * 200 5 0
         * 500 4 0
         * 400 4 0
         *
         * expect 6200
         * @param args
         */
    
        public static void main(String[] args){
            Scanner sc = new Scanner(System.in);
            int N = sc.nextInt();
            int m = sc.nextInt();
    
            Goods[] goods = new Goods[m];
            for(int i = 0; i < m; i++){
                goods[i] = new Goods();
            }
            for(int i = 0; i < m; i++){
                int v = sc.nextInt();
                int p = sc.nextInt();
                int q = sc.nextInt();
                goods[i].v = v;
                // 直接用p*v，方便后面计算
                goods[i].p = p * v;
                if(q==0){
                    goods[i].main = true;
                }else if(goods[q-1].a1 == -1){
                    goods[q-1].a1 = i;
                }else{
                    goods[q-1].a2 = i;
                }
            }
    
            int[][] dp = new int[m+1][N+1];
            for(int i = 1; i <= m; i++){
                for(int j = 0; j <= N; j++){
                    dp[i][j] = dp[i-1][j];
                    if(!goods[i-1].main){
                        continue;
                    }
                    if(j>=goods[i-1].v){
                        dp[i][j] = Math.max(dp[i][j], dp[i-1][j-goods[i-1].v] + goods[i-1].p);
                    }
                    if(goods[i-1].a1 != -1 && j >= goods[i-1].v + goods[goods[i-1].a1].v){
                        dp[i][j] = Math.max(dp[i][j], dp[i-1][j-goods[i-1].v - goods[goods[i-1].a1].v] + goods[i-1].p + goods[goods[i-1].a1].p);
                    }
                    if(goods[i-1].a2 != -1 && j >= goods[i-1].v + goods[goods[i-1].a2].v){
                        dp[i][j] = Math.max(dp[i][j], dp[i-1][j-goods[i-1].v - goods[goods[i-1].a2].v] + goods[i-1].p + goods[goods[i-1].a2].p);
                    }
                    if(goods[i-1].a1 != -1 && goods[i-1].a2 != -1 &&  j >= goods[i-1].v + goods[goods[i-1].a1].v + goods[goods[i-1].a2].v){
                        dp[i][j] = Math.max(dp[i][j], dp[i-1][j-goods[i-1].v - goods[goods[i-1].a1].v - goods[goods[i-1].a2].v] + goods[i-1].p + goods[goods[i-1].a1].p + goods[goods[i-1].a2].p);
                    }
                }
            }
            System.out.println(dp[m][N]);
        }
    
        private static class Goods {
            int v;
            int p;
            boolean main = false;
    
            int a1 = -1;  //定义附件1的编号
            int a2 = -1;  //定义附件2的编号
        }
    
    
    
        
        
        
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        int N = in.nextInt();
    //        int m = in.nextInt();
    //
    //        Node[] products = new Node[m+1];
    //        List<Node> sortProducts = new ArrayList<Node>();
    //
    //        for(int i=1; i<=m; i++){
    //            int v = in.nextInt();
    //            int p = in.nextInt();
    //            int q = in.nextInt();
    //
    //            // Node tmp = new Node(v, p, q, i);
    //            products[i] = new Node(v, p, q, i);
    //            sortProducts.add(new Node(v, p, q, i));
    //        }
    //
    ////        Collections.sort(sortProducts, new Comparator<Node>(){
    ////            @Override
    ////            public int compare(Node o1, Node o2){
    ////                return (o2.getSatisfaction() - o1.getSatisfaction());
    ////            }
    ////        });
    //
    //        Collections.sort(sortProducts, (o1, o2) -> (o2.getSatisfaction() - o1.getSatisfaction()));
    //
    //        // int balance = 0;
    //        // int count = 0;
    //        int result = 0;
    //
    //        // Node[] sorted = sortProducts.;
    //
    //        for(int i=0; i<m; i++){
    //            int balance = N;
    //            int count = 0;
    //            int j = i;
    //            int max = 0;
    //            Set<Integer> bought = new HashSet<>();
    //            while(j<m && balance > 0){
    //                Node node = sortProducts.get(j++);
    //                if(!bought.contains(node.index)){
    //                    // if(node.getV() <= balance){
    //                    if(node.getV() <= balance){
    //                        // if(!bought.contains(node.index)){
    //                        bought.add(node.index);
    //                        max += node.getSatisfaction();
    //                        balance -= node.getV();
    //                    }else{
    //                        break;
    //                    }
    //
    //                    if(node.getQ() > 0){
    //                        if(!bought.contains(node.getQ())){
    //                            // if(products[node.getQ()].getV() <= balance){
    //                            if(products[node.getQ()].getV() <= balance){
    //                                // if(!bought.contains(node.getQ())){
    //                                bought.add(node.getQ());
    //                                max += products[node.getQ()].getSatisfaction();
    //                                balance -= products[node.getQ()].getV();
    //                            }else{
    //                                break;
    //                            }
    //                        }else{
    //                            // continue;
    //                        }
    //                    }
    //                }else{
    //                    // continue;
    //                }
    //
    //                result = (result<max) ? max : result;
    //            }
    //
    //        }
    //
    //        System.out.print(result);
    //
    //        // Collections.sort(sortProducts, new Comparator<Node>(){
    //        //     @Override
    //        //     public int Compare(Node o1, Node o2){
    //        //         return (o2.getSatisfaction() - o1.getSatisfaction());
    //        //     }
    //        // });
    //
    //
    //
    //        // // 注意 hasNext 和 hasNextLine 的区别
    //        // while (in.hasNextInt()) { // 注意 while 处理多个 case
    //        //     int a = in.nextInt();
    //        //     int b = in.nextInt();
    //        //     System.out.println(a + b);
    //        // }
    //    }
    //
    //    private static class Node{
    //        public int v;
    //        public int p;
    //        public int q;
    //
    //        public int index;
    //        public int satisfaction;
    //
    //        public Node(int v, int p, int q, int index){
    //            this.v = v;
    //            this.p = p;
    //            this.q = q;
    //            this.index = index;
    //            this.satisfaction = ***bsp;       }
    //
    //        public int getV(){
    //            return this.v;
    //        }
    //
    //        public int getP(){
    //            return this.p;
    //        }
    //
    //        public int getQ(){
    //            return this.q;
    //        }
    //
    //        public int getSatisfaction(){
    //            return this.satisfaction;
    //        }
    //
    //        // int compare(Node o1, Node o2){
    //        //     return (o2.getSatisfaction() - o1.getSatisfaction());
    //        // }
    //    }
    }

  

