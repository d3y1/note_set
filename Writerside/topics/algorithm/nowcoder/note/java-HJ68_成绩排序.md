# java-HJ68 成绩排序

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;
import java.util.PriorityQueue;
import java.util.Scanner;
import java.util.stream.Collectors;

/**
 * HJ68 成绩排序
 * @author d3y1
 */
public class Main {
    public static void main(String[] args) {
        // solution1();
        // solution2();
        // solution3();
        // solution4();
        // solution5();
        // solution6();
        solution7();
    }

    /**
     * List.sort() - lambda
     */
    private static void solution1(){
        Scanner in = new Scanner(System.in);
        int N = in.nextInt();
        int sort = in.nextInt();

        List<Student> studentList = new ArrayList<>();
        for(int i=1; i<=N; i++){
            String name = in.next();
            Integer score = in.nextInt();
            studentList.add(new Student(name, score));
        }

        // desc - default stable
        if(sort == 0){
            studentList.sort((o1, o2) -> o2.getScore() - o1.getScore());
        }
        // asc - default stable
        else if(sort == 1){
            studentList.sort((o1, o2) -> o1.getScore() - o2.getScore());
        }

        for(Student student: studentList){
            System.out.println(student.toString());
        }
    }

    /**
     * List.sort() - Comparator.comparingInt()
     */
    private static void solution2(){
        Scanner in = new Scanner(System.in);
        int N = in.nextInt();
        int sort = in.nextInt();

        List<Student> studentList = new ArrayList<>();
        for(int i=1; i<=N; i++){
            String name = in.next();
            Integer score = in.nextInt();
            studentList.add(new Student(name, score));
        }

        // desc - default stable
        if(sort == 0){
            studentList.sort(Comparator.comparingInt(Student::getScore).reversed());
        }
        // asc - default stable
        else if(sort == 1){
            studentList.sort(Comparator.comparingInt(Student::getScore));
        }

        for(Student student: studentList){
            System.out.println(student.toString());
        }
    }

    /**
     * List.sort() - List.stream().sorted(Comparator.comparing()).collect()
     */
    private static void solution3(){
        Scanner in = new Scanner(System.in);
        int N = in.nextInt();
        int sort = in.nextInt();

        List<Student> studentList = new ArrayList<>();
        for(int i=1; i<=N; i++){
            String name = in.next();
            Integer score = in.nextInt();
            studentList.add(new Student(name, score));
        }

        // desc - default stable
        if(sort == 0){
            studentList = studentList.stream().sorted(Comparator.comparing(Student::getScore).reversed()).collect(Collectors.toList());
        }
        // asc - default stable
        else if(sort == 1){
            studentList = studentList.stream().sorted(Comparator.comparing(Student::getScore)).collect(Collectors.toList());
        }

        for(Student student: studentList){
            System.out.println(student.toString());
        }
    }

    /**
     * List.sort() - Comparator<Student>
     */
    private static void solution4(){
        Scanner in = new Scanner(System.in);
        int N = in.nextInt();
        int sort = in.nextInt();

        List<Student> studentList = new ArrayList<>();
        for(int i=1; i<=N; i++){
            String name = in.next();
            Integer score = in.nextInt();
            studentList.add(new Student(name, score));
        }

        // desc - default stable
        if(sort == 0){
            studentList.sort(new Comparator<Student>(){
                @Override
                public int compare(Student o1, Student o2){
                    return o2.getScore() - o1.getScore();
                }
            });
        }
        // asc - default stable
        else if(sort == 1){
            studentList.sort(new Comparator<Student>(){
                @Override
                public int compare(Student o1, Student o2){
                    return o1.getScore() - o2.getScore();
                }
            });
        }

        for(Student student: studentList){
            System.out.println(student.toString());
        }
    }

    /**
     * List.sort() - Student.INCREASE & Student.DECREASE
     */
    private static void solution5(){
        Scanner in = new Scanner(System.in);
        int N = in.nextInt();
        int sort = in.nextInt();

        List<Student> studentList = new ArrayList<>();
        for(int i=1; i<=N; i++){
            String name = in.next();
            Integer score = in.nextInt();
            studentList.add(new Student(name, score));
        }

        // desc - default stable
        if(sort == 0){
            studentList.sort(Student.DECREASE);
        }
        // asc - default stable
        else if(sort == 1){
            studentList.sort(Student.INCREASE);
        }

        for(Student student: studentList){
            System.out.println(student.toString());
        }
    }

    private static class Student {
        private String name;
        private Integer score;

        private static final Comparator<Student> INCREASE = new increase();
        private static final Comparator<Student> DECREASE = new decrease();

        public String getName(){
            return name;
        }

        public Integer getScore(){
            return score;
        }

        public Student(String name, Integer score){
            this.name = name;
            this.score = score;
        }

        public static class increase implements Comparator<Student>{
            @Override
            public int compare(Student o1, Student o2){
                return o1.getScore() - o2.getScore();
            }
        }

        public static class decrease implements Comparator<Student> {
            @Override
            public int compare(Student o1, Student o2){
                return o2.getScore() - o1.getScore();
            }
        }

        @Override
        public String toString(){
            return name + " " + score;
        }
    }

    ////////////////////////////////////////////////////////////////////////////////////////

    /**
     * 堆排序: 错误!(不稳定)
     */
    private static void solution6(){
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();
        int order = in.nextInt();
        PriorityQueue<Student> heap;
        if(order == 0){
            heap = new PriorityQueue<>((o1,o2) -> (o2.score-o1.score));
        }else{
            heap = new PriorityQueue<>();
        }

        in.nextLine();
        String[] parts;
        for(int i=0; i<n; i++){
            parts = in.nextLine().trim().split(" ");
            heap.offer(new Student(parts[0], Integer.parseInt(parts[1])));
        }

        Student top;
        while(!heap.isEmpty()){
            top = heap.poll();
            System.out.println(top.name+" "+top.score);
        }
    }

    /**
     * 排序: ArrayList
     */
    private static void solution7(){
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();
        int order = in.nextInt();

        in.nextLine();
        ArrayList<Student> list = new ArrayList<>();
        String[] parts;
        for(int i=0; i<n; i++){
            parts = in.nextLine().trim().split(" ");
            list.add(new Student(parts[0], Integer.valueOf(parts[1])));
        }

        // 稳定
        if(order == 0){
            Collections.sort(list, (o1, o2) -> (o2.score-o1.score));
        }else{
            Collections.sort(list, (o1,o2) -> (o1.score-o2.score));
        }

        // for(int i=0; i<n; i++){
        //     System.out.println(list.get(i).name+" "+list.get(i).score);
        // }
        for(Student student: list){
            System.out.println(student.toString());
        }
    }
}
```
