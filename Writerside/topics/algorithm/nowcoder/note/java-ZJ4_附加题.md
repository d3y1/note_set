# java-ZJ4 附加题


    import java.util.Scanner;
    
    public class Main {
        private static int max = 0;
        private static int[] nums = new int[24];
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法: 3轴旋转(xyz)
         * @param in
         */
        private static void solution(Scanner in){
            max = 0;
            nums = new int[24];
    
            for(int i=0; i<24; i++){
                nums[i] = in.nextInt();
            }
    
            // init magic cube
            int[][] matrix = new int[9][7];
            matrix[1][3] = 0;
            matrix[1][4] = 1;
    
            matrix[2][3] = 2;
            matrix[2][4] = 3;
    
            matrix[3][1] = 4;
            matrix[3][2] = 5;
            matrix[3][3] = 6;
            matrix[3][4] = 7;
            matrix[3][5] = 8;
            matrix[3][6] = 9;
    
            matrix[4][1] = 10;
            matrix[4][2] = 11;
            matrix[4][3] = 12;
            matrix[4][4] = 13;
            matrix[4][5] = 14;
            matrix[4][6] = 15;
    
            matrix[5][3] = 16;
            matrix[5][4] = 17;
    
            matrix[6][3] = 18;
            matrix[6][4] = 19;
    
            matrix[7][3] = 20;
            matrix[7][4] = 21;
    
            matrix[8][3] = 22;
            matrix[8][4] = 23;
    
            operate(0, matrix);
    
            System.out.println(max);
        }
    
        /**
         * 递归
         * @param opTimes
         * @param matrix
         */
        private static void operate(int opTimes, int[][] matrix){
            if(opTimes <= 5){
                max = Math.max(max, beauty(matrix));
            }else{
                return;
            }
    
            // 1-xy平面(绕z轴旋转) 2-yz平面(绕x轴旋转) 3-xz平面(绕y轴旋转)
            for(int i=1; i<=3; i++){
                // 1-左右旋转(xy平面,绕z轴旋转)
                if(i == 1){
                    // 0-向左旋转 1-向右旋转
                    for(int j=0; j<=1; j++){
                        rotate(i, j, matrix);
                        operate(opTimes+1, matrix);
                        rotate(i, (j+1)%2, matrix);
                    }
                }
    
                // 2-上下旋转(yz平面,绕x轴旋转)
                if(i == 2){
                    // 0-向上旋转 1-向下旋转
                    for(int j=0; j<=1; j++){
                        rotate(i, j, matrix);
                        operate(opTimes+1, matrix);
                        rotate(i, (j+1)%2, matrix);
                    }
                }
    
                // 3-顺逆旋转(xz平面,绕y轴旋转)
                if(i == 3){
                    // 0-顺时针旋转 1-逆时针旋转
                    for(int j=0; j<=1; j++){
                        rotate(i, j, matrix);
                        operate(opTimes+1, matrix);
                        rotate(i, (j+1)%2, matrix);
                    }
                }
            }
        }
    
        /**
         * 旋转: 以序号6 7 12 13所在平面为基准
         * @param i
         * @param j
         * @param matrix
         */
        private static void rotate(int i, int j, int[][] matrix){
            // 1-左右旋转(xy平面,绕z轴旋转)
            if(i == 1){
                zRotate(j, matrix);
            }
    
            // 2-上下旋转(yz平面,绕x轴旋转)
            if(i == 2){
                xRotate(j, matrix);
            }
    
            // 3-顺逆旋转(xz平面,绕y轴旋转)
            if(i == 3){
                yRotate(j, matrix);
            }
        }
    
        /**
         * 上下旋转(yz平面,绕x轴旋转)
         * 左列向上旋转 等价于 右列向下旋转, 右列可不管
         * @param j
         * @param matrix
         */
        private static void xRotate(int j, int[][] matrix){
            // 左列(序号6 12所在yz平面) 向上旋转
            if(j == 0){
                int tmp1 = matrix[1][3];
                int tmp2 = matrix[2][3];
    
                matrix[1][3] = matrix[3][3];
                matrix[2][3] = matrix[4][3];
    
                matrix[3][3] = matrix[5][3];
                matrix[4][3] = matrix[6][3];
    
                matrix[5][3] = matrix[7][3];
                matrix[6][3] = matrix[8][3];
    
                matrix[7][3] = tmp1;
                matrix[8][3] = tmp2;
    
                // 面(序号4 5 10 11平面) 旋转
                int tmp3 = matrix[3][1];
                matrix[3][1] = matrix[3][2];
                matrix[3][2] = matrix[4][2];
                matrix[4][2] = matrix[4][1];
                matrix[4][1] = tmp3;
            }
    
            // 左列(序号6 12所在yz平面) 向下旋转
            if(j == 1){
                int tmp1 = matrix[8][3];
                int tmp2 = matrix[7][3];
    
                matrix[8][3] = matrix[6][3];
                matrix[7][3] = matrix[5][3];
    
                matrix[6][3] = matrix[4][3];
                matrix[5][3] = matrix[3][3];
    
                matrix[4][3] = matrix[2][3];
                matrix[3][3] = matrix[1][3];
    
                matrix[2][3] = tmp1;
                matrix[1][3] = tmp2;
    
                // 面(序号4 5 10 11平面) 旋转
                int tmp3 = matrix[3][1];
                matrix[3][1] = matrix[4][1];
                matrix[4][1] = matrix[4][2];
                matrix[4][2] = matrix[3][2];
                matrix[3][2] = tmp3;
            }
        }
    
        /**
         * 顺逆旋转(xz平面,绕y轴旋转)
         * @param j
         * @param matrix
         */
        private static void yRotate(int j, int[][] matrix){
            // (序号6 7 12 13所在xz平面) 顺时针旋转
            if(j == 0){
                int tmp1 = matrix[2][3];
                int tmp2 = matrix[2][4];
    
                matrix[2][3] = matrix[4][2];
                matrix[2][4] = matrix[3][2];
    
                matrix[4][2] = matrix[5][4];
                matrix[3][2] = matrix[5][3];
    
                matrix[5][4] = matrix[3][5];
                matrix[5][3] = matrix[4][5];
    
                matrix[3][5] = tmp1;
                matrix[4][5] = tmp2;
    
                // 面 旋转
                int tmp3 = matrix[3][3];
                matrix[3][3] = matrix[4][3];
                matrix[4][3] = matrix[4][4];
                matrix[4][4] = matrix[3][4];
                matrix[3][4] = tmp3;
            }
    
            // (序号6 7 12 13所在xz平面) 逆时针旋转
            if(j == 1){
                int tmp1 = matrix[2][3];
                int tmp2 = matrix[2][4];
    
                matrix[2][3] = matrix[3][5];
                matrix[2][4] = matrix[4][5];
    
                matrix[3][5] = matrix[5][4];
                matrix[4][5] = matrix[5][3];
    
                matrix[5][4] = matrix[4][2];
                matrix[5][3] = matrix[3][2];
    
                matrix[4][2] = tmp1;
                matrix[3][2] = tmp2;
    
                // 面 旋转
                int tmp3 = matrix[3][3];
                matrix[3][3] = matrix[3][4];
                matrix[3][4] = matrix[4][4];
                matrix[4][4] = matrix[4][3];
                matrix[4][3] = tmp3;
            }
        }
    
        /**
         * 左右旋转(xy平面,绕z轴旋转)
         * 上行向左旋转 等价于 下行向右旋转, 下行可不管
         * @param j
         * @param matrix
         */
        private static void zRotate(int j, int[][] matrix){
            // 上行(序号6 7所在xy平面) 向左旋转
            if(j == 0){
                // 行 旋转
                int tmp1 = matrix[3][1];
                int tmp2 = matrix[3][2];
    
                matrix[3][1] = matrix[3][3];
                matrix[3][2] = matrix[3][4];
    
                matrix[3][3] = matrix[3][5];
                matrix[3][4] = matrix[3][6];
    
                matrix[3][5] = matrix[8][4];
                matrix[3][6] = matrix[8][3];
    
                matrix[8][4] = tmp1;
                matrix[8][3] = tmp2;
    
                // 面(序号0 1 2 3平面) 旋转
                int tmp3 = matrix[1][3];
                matrix[1][3] = matrix[2][3];
                matrix[2][3] = matrix[2][4];
                matrix[2][4] = matrix[1][4];
                matrix[1][4] = tmp3;
            }
    
            // 上行(序号6 7所在xy平面) 向右旋转
            if(j == 1){
                int tmp1 = matrix[3][6];
                int tmp2 = matrix[3][5];
    
                matrix[3][6] = matrix[3][4];
                matrix[3][5] = matrix[3][3];
    
                matrix[3][4] = matrix[3][2];
                matrix[3][3] = matrix[3][1];
    
                matrix[3][2] = matrix[8][3];
                matrix[3][1] = matrix[8][4];
    
                matrix[8][3] = tmp1;
                matrix[8][4] = tmp2;
    
                // 面(序号0 1 2 3平面) 旋转
                int tmp3 = matrix[1][3];
                matrix[1][3] = matrix[1][4];
                matrix[1][4] = matrix[2][4];
                matrix[2][4] = matrix[2][3];
                matrix[2][3] = tmp3;
            }
        }
    
        private static int beauty(int[][] matrix){
            int beauty1 = nums[matrix[1][3]] * nums[matrix[1][4]] * nums[matrix[2][3]] * nums[matrix[2][4]];
            int beauty2 = nums[matrix[3][1]] * nums[matrix[3][2]] * nums[matrix[4][1]] * nums[matrix[4][2]];
            int beauty3 = nums[matrix[3][3]] * nums[matrix[3][4]] * nums[matrix[4][3]] * nums[matrix[4][4]];
            int beauty4 = nums[matrix[3][5]] * nums[matrix[3][6]] * nums[matrix[4][5]] * nums[matrix[4][6]];
            int beauty5 = nums[matrix[5][3]] * nums[matrix[5][4]] * nums[matrix[6][3]] * nums[matrix[6][4]];
            int beauty6 = nums[matrix[7][3]] * nums[matrix[7][4]] * nums[matrix[8][3]] * nums[matrix[8][4]];
    
            return beauty1+beauty2+beauty3+beauty4+beauty5+beauty6;
        }
    }

  

