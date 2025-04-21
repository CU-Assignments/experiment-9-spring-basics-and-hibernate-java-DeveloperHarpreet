import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

class Course {
    private String courseName;
    private int duration;

    public Course(String courseName, int duration) {
        this.courseName = courseName;
        this.duration = duration;
    }

    public String getCourseName() {
        return courseName;
    }

    public int getDuration() {
        return duration;
    }

    public String toString() {
        return "Course: " + courseName + ", Duration: " + duration + " weeks";
    }
}

class Student {
    private String name;
    private Course course;

    public Student(String name, Course course) {
        this.name = name;
        this.course = course;
    }

    public String toString() {
        return "Student: " + name + "\n" + course.toString();
    }
}

@Configuration
class AppConfig {
    @Bean
    public Course course() {
        return new Course("Java Programming", 12);
    }

    @Bean
    public Student student() {
        return new Student("Alice", course());
    }
}

public class EasyLevelSpringDI {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        Student student = context.getBean(Student.class);
        System.out.println(student);
    }
}
