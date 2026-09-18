# 115_1_Java

紀錄"物件導向程式設計與AI協作"

public class HelloCourse {
    public static void main(String[] args) {
        // 固定輸出，方便比較不同工具的執行結果。
        System.out.println("Hello, Java!");
        System.out.println("Course: Object-Oriented Programming");
    }
}
javac -encoding UTF-8 -d out src/HelloCourse.java
java -cp out HelloCourse
