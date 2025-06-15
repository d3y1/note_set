# java-ZJ13 最大点集


    import java.io.BufferedReader;
    import java.io.IOException;
    import java.io.InputStreamReader;
    import java.util.ArrayList;
    import java.util.List;
    
    public class Main {
        public static void main(String[] args) throws IOException{
            BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
    
            solution(reader);
        }
    
        /**
         * 模拟法
         *
         * List<Point> pointList = new ArrayList<>()
         *
         * BufferedReader reader = new BufferedReader(new InputStreamReader(System.in))
         * Scanner in = new Scanner(System.in) -> 比BufferedReader多花大约700ms时间
         *
         * @param reader
         */
        private static void solution(BufferedReader reader) throws IOException{
            int N = Integer.parseInt(reader.readLine());
    
            List<Point> pointList = new ArrayList<>();
    
            Point xMaxPoint = new Point(0, 0);
            Point yMaxPoint = new Point(0, 0);
            StringBuilder sb = new StringBuilder();
            int x,y;
            String[] line;
            for(int i=1; i<=N; i++){
                line = reader.readLine().split(" ");
                x = Integer.parseInt(line[0]);
                y = Integer.parseInt(line[1]);
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
                sb.append(xMaxPoint.toString());
            }else{
                int tmpMaxY = xMaxPoint.y;
                sb.append(xMaxPoint.toString());
    
                pointList.sort((o1, o2) -> {
                    if(o1.x != o2.x){
                        return o2.x - o1.x;
                    }else{
                        return o1.y - o2.y;
                    }
                });
    
                Point point;
                int size = pointList.size();
                for(int i=1; i<size; i++){
                    point = pointList.get(i);
                    if(point.y >= tmpMaxY){
                        tmpMaxY = point.y;
                        sb.insert(0, point.toString()+"\n");
                        if(point.equals(yMaxPoint)){
                            break;
                        }
                    }
                }
            }
    
            System.out.println(sb);
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
    
            @Override
            public String toString(){
                return x+" "+y;
            }
    
            public Point(int x, int y){
                this.x = x;
                this.y = y;
            }
        }
    }

  

