# java-ZJ11 编程题1


    import java.io.BufferedReader;
    import java.io.BufferedWriter;
    import java.io.IOException;
    import java.io.InputStreamReader;
    import java.io.OutputStreamWriter;
    import java.util.ArrayList;
    import java.util.Arrays;
    import java.util.List;
    import java.util.Scanner;
    
    public class Main {
        //    public static void main(String[] args){
    //        Scanner in = new Scanner(System.in);
    //
    //        while(in.hasNext()){
    //            solution1(in);
    //            solution2(in);
    //            solution3(in);
    //        }
    //    }
    
        /**
         * 模拟法: BufferedReader+BufferedWriter -> 偶尔通过!
         * @param args
         * @throws IOException
         */
        public static void main(String[] args) throws IOException{
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    
            int N = Integer.parseInt(br.readLine());
    
            int[][] points = new int[N][2];
            for(int i=0; i<N; i++){
                String[] point = br.readLine().trim().split(" ");
                points[i][0] = Integer.parseInt(point[0]);
                points[i][1] = Integer.parseInt(point[1]);
            }
    
            Arrays.sort(points, (o1, o2) -> o2[1] - o1[1]);
    
            int maxX = 0;
            for(int i=0; i<N; i++){
                if(points[i][0] >= maxX){
                    maxX = points[i][0];
                    bw.write(points[i][0]+" "+points[i][1]);
                    bw.newLine();
                }
            }
            bw.flush();
        }
    
        /**
         * 模拟法
         *
         * int[][] pointList = new int[N][2]
         *
         * @param in
         */
        private static void solution1(Scanner in){
            int N = in.nextInt();
    
            int[][] pointList = new int[N][2];
    
            Point xMaxPoint = new Point(0, 0);
            Point yMaxPoint = new Point(0, 0);
            List<Point> resultList = new ArrayList<>();
            int x,y;
            for(int i=0; i<N; i++){
                x = in.nextInt();
                y = in.nextInt();
                if(x>xMaxPoint.x || (x==xMaxPoint.x && y<xMaxPoint.y)){
                    xMaxPoint.setX(x);
                    xMaxPoint.setY(y);
                }
                if(y>yMaxPoint.y || (y==yMaxPoint.y && x<yMaxPoint.x)){
                    yMaxPoint.setX(x);
                    yMaxPoint.setY(y);
                }
                pointList[i][0] = x;
                pointList[i][1] = y;
            }
    
            if(xMaxPoint.equals(yMaxPoint)){
                resultList.add(xMaxPoint);
            }else{
                Point tmp = new Point(xMaxPoint.x, xMaxPoint.y);
                resultList.add(xMaxPoint);
                Arrays.sort(pointList, (o1, o2) -> {
                    if(o1[0] != o2[0]){
                        return o2[0] - o1[0];
                    }else{
                        return o1[1] - o2[1];
                    }
                });
    
                for(int i=1; i<N; i++){
                    if(pointList[i][0]>=yMaxPoint.x && (tmp.y<=pointList[i][1] && pointList[i][1]<=yMaxPoint.y)){
                        tmp = new Point(pointList[i][0], pointList[i][1]);
                        resultList.add(0, tmp);
                        if(tmp.equals(yMaxPoint)){
                            break;
                        }
                    }
                }
            }
    
            for(Point point: resultList){
                System.out.println(point.x+" "+point.y);
            }
        }
    
    
        /**
         * 模拟法
         *
         * Point[] pointList = new Point[N]
         *
         * @param in
         */
        private static void solution2(Scanner in){
            int N = in.nextInt();
    
            Point[] pointList = new Point[N];
    
            Point xMaxPoint = new Point(0, 0);
            Point yMaxPoint = new Point(0, 0);
            List<Point> resultList = new ArrayList<>();
            int x,y;
            for(int i=0; i<N; i++){
                x = in.nextInt();
                y = in.nextInt();
                if(x>xMaxPoint.x || (x==xMaxPoint.x && y<xMaxPoint.y)){
                    xMaxPoint.setX(x);
                    xMaxPoint.setY(y);
                }
                if(y>yMaxPoint.y || (y==yMaxPoint.y && x<yMaxPoint.x)){
                    yMaxPoint.setX(x);
                    yMaxPoint.setY(y);
                }
                pointList[i] = new Point(x, y);
            }
    
            if(xMaxPoint.equals(yMaxPoint)){
                resultList.add(xMaxPoint);
            }else{
                Point tmp = new Point(xMaxPoint.x, xMaxPoint.y);
                resultList.add(xMaxPoint);
                Arrays.sort(pointList, (o1, o2) -> {
                    if(o1.x != o2.x){
                        return o2.x - o1.x;
                    }else{
                        return o1.y - o2.y;
                    }
                });
    
                for(int i=1; i<N; i++){
                    if(pointList[i].x>=yMaxPoint.x && (tmp.y<=pointList[i].y && pointList[i].y<=yMaxPoint.y)){
                        tmp = new Point(pointList[i].x, pointList[i].y);
                        resultList.add(0, tmp);
                        if(tmp.equals(yMaxPoint)){
                            break;
                        }
                    }
                }
            }
    
            for(Point point: resultList){
                System.out.println(point.x+" "+point.y);
            }
        }
    
    
        /**
         * 模拟法
         *
         * List<Point> pointList = new ArrayList<>()
         *
         * @param in
         */
        private static void solution3(Scanner in){
            int N = in.nextInt();
    
            List<Point> pointList = new ArrayList<>();
    
            Point xMaxPoint = new Point(0, 0);
            Point yMaxPoint = new Point(0, 0);
            List<Point> resultList = new ArrayList<>();
            int x,y;
            for(int i=1; i<=N; i++){
                x = in.nextInt();
                y = in.nextInt();
                if(x>xMaxPoint.x || (x==xMaxPoint.x && y<xMaxPoint.y)){
                    xMaxPoint.setX(x);
                    xMaxPoint.setY(y);
                }
                if(y>yMaxPoint.y || (y==yMaxPoint.y && x<yMaxPoint.x)){
                    yMaxPoint.setX(x);
                    yMaxPoint.setY(y);
                }
                pointList.add(new Point(x, y));
            }
    
            if(xMaxPoint.equals(yMaxPoint)){
                resultList.add(xMaxPoint);
            }else{
                Point tmp = new Point(xMaxPoint.x, xMaxPoint.y);
                resultList.add(xMaxPoint);
    
                pointList.sort((o1, o2) -> {
                    if(o1.x != o2.x){
                        return o2.x - o1.x;
                    }else{
                        return o1.y - o2.y;
                    }
                });
    
                for(int i=1; i<pointList.size(); i++){
                    if(pointList.get(i).x>=yMaxPoint.x && (tmp.y<=pointList.get(i).y && pointList.get(i).y<=yMaxPoint.y)){
                        tmp = new Point(pointList.get(i).x, pointList.get(i).y);
                        resultList.add(0, tmp);
                        if(tmp.equals(yMaxPoint)){
                            break;
                        }
                    }
                }
            }
    
            for(Point point: resultList){
                System.out.println(point.x+" "+point.y);
            }
        }
    
        private static class Point{
            int x;
            int y;
    
            public int getX(){
                return x;
            }
    
            public void setX(int x){
                this.x = x;
            }
    
            public int getY(){
                return y;
            }
    
            public void setY(int y){
                this.y = y;
            }
    
            @Override
            public boolean equals(Object o){
                if(this == o){
                    return true;
                }
                if(o == null || getClass() != o.getClass()){
                    return false;
                }
                Point point = (Point) o;
                return x == point.x && y == point.y;
            }
    
            public Point(int x, int y){
                this.x = x;
                this.y = y;
            }
        }
    }

  

