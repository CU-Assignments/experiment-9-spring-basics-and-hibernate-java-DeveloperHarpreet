import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.Table;
import jakarta.persistence.Column;
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration as SpringConfiguration;
import org.springframework.transaction.annotation.EnableTransactionManagement;

@Entity
@Table(name = "Account")
class Account {
    @Id
    private int accountId;

    @Column
    private String accountHolderName;

    @Column
    private double balance;

    public Account() {} 
    public Account(int accountId, String accountHolderName, double balance) {
        this.accountId = accountId;
        this.accountHolderName = accountHolderName;
        this.balance = balance;
    }

    public int getAccountId() { return accountId; }
    public void setAccountId(int accountId) { this.accountId = accountId; }

    public String getAccountHolderName() { return accountHolderName; }
    public void setAccountHolderName(String accountHolderName) { this.accountHolderName = accountHolderName; }

    public double getBalance() { return balance; }
    public void setBalance(double balance) { this.balance = balance; }
}

@SpringConfiguration
@EnableTransactionManagement
class AppConfig {
    @Bean
    public SessionFactory sessionFactory() {
        Configuration cfg = new Configuration();
        cfg.configure("hibernate.cfg.xml");
        cfg.addAnnotatedClass(Account.class);
        return cfg.buildSessionFactory();
    }
}

public class HardLevelSpringHibernateTransaction {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        SessionFactory factory = context.getBean(SessionFactory.class);

        Session session = factory.openSession();

        Transaction tx = session.beginTransaction();
        Account acc1 = new Account(101, "Alice", 5000);
        Account acc2 = new Account(102, "Bob", 3000);
        session.save(acc1);
        session.save(acc2);
        tx.commit();

        System.out.println("Accounts created successfully!");
        session = factory.openSession();
        tx = session.beginTransaction();

        try {
            Account sender = session.get(Account.class, 101);
            Account receiver = session.get(Account.class, 102);

            double transferAmount = 1000;

            if (sender.getBalance() >= transferAmount) {
                sender.setBalance(sender.getBalance() - transferAmount);
                receiver.setBalance(receiver.getBalance() + transferAmount);

                session.update(sender);
                session.update(receiver);

                tx.commit();
                System.out.println("Transaction Successful: $" + transferAmount + " transferred from " + sender.getAccountHolderName() + " to " + receiver.getAccountHolderName());
            } else {
                System.out.println("Transaction Failed: Insufficient funds.");
                tx.rollback();
            }
        } catch (Exception e) {
            tx.rollback();
            e.printStackTrace();
        } finally {
            session.close();
        }

        factory.close();
        context.close();
    }
}
