import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.Table;
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

@Entity
@Table(name = "Student")
class Student {
    @Id
    private int id;
    private String name;
    private int age;

    public Student() {}  

    public Student(int id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }

    public int getId() { return id; }
    public void setId(int id) { this.id = id; }

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }

    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }
}

public class MediumLevelHibernateCRUD {
    public static void main(String[] args) {
        Configuration cfg = new Configuration();
        cfg.configure("hibernate.cfg.xml"); 
        cfg.addAnnotatedClass(Student.class); 
        SessionFactory factory = cfg.buildSessionFactory();

        Session session = factory.openSession();
        Transaction tx = session.beginTransaction();

        Student newStudent = new Student(1, "John Wick", 35);
        session.save(newStudent);

        tx.commit();
        session.close();

        System.out.println("Student inserted successfully!");

        session = factory.openSession();
        Student fetched = session.get(Student.class, 1);
        System.out.println("Fetched Student: " + fetched.getName() + ", Age: " + fetched.getAge());
        session.close();

        session = factory.openSession();
        tx = session.beginTransaction();
        fetched.setAge(36);
        session.update(fetched);
        tx.commit();
        session.close();
        System.out.println("Student updated successfully!");

        session = factory.openSession();
        tx = session.beginTransaction();
        session.delete(fetched);
        tx.commit();
        session.close();
        System.out.println("Student deleted successfully!");

        factory.close();
    }
}
