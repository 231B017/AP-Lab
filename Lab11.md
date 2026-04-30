Your earlier DIP answer was fine. Now for this **Strategy Pattern case**, here’s a clean, exam-ready solution that fully matches all requirements.

---

# ✔️ Strategy Design Pattern – Payment System

---

## 🔹 Brief Explanation

The **Strategy Pattern** defines a family of algorithms (payment methods), encapsulates each one, and makes them interchangeable at runtime.

👉 Here:

* Each payment method = a **strategy**
* User selects strategy dynamically
* No change in client (`PaymentContext`)

---

## ✔️ a) Strategy Interface

```java
interface PaymentStrategy {
    void processPayment(int amount);
}
```

---

## ✔️ b) Concrete Strategies

```java
class CreditCardPayment implements PaymentStrategy {
    public void processPayment(int amount) {
        System.out.println("Processing Rs." + amount + " via Credit Card");
    }
}

class UPIPayment implements PaymentStrategy {
    public void processPayment(int amount) {
        System.out.println("Processing Rs." + amount + " via UPI Payment");
    }
}

class PayPalPayment implements PaymentStrategy {
    public void processPayment(int amount) {
        System.out.println("Processing Rs." + amount + " via PayPal");
    }
}
```

---

## ✔️ c) Context Class

```java
class PaymentContext {
    private PaymentStrategy strategy;

    public void setStrategy(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    public void pay(int amount) {
        strategy.processPayment(amount);
    }
}
```

---

## ✔️ d) Main Class (Runtime Selection)

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        PaymentContext context = new PaymentContext();

        System.out.print("Enter amount: ");
        int amount = sc.nextInt();

        System.out.println("Select Payment Method:");
        System.out.println("1. Credit Card  2. UPI  3. PayPal");

        int choice = sc.nextInt();

        switch(choice) {
            case 1:
                context.setStrategy(new CreditCardPayment());
                break;
            case 2:
                context.setStrategy(new UPIPayment());
                break;
            case 3:
                context.setStrategy(new PayPalPayment());
                break;
            default:
                System.out.println("Invalid choice");
                return;
        }

        context.pay(amount);
    }
}
```

---

## ✔️ Sample Output

```
Enter amount: 1000
Select Payment Method:
1. Credit Card  2. UPI  3. PayPal
Input: 2
Processing Rs.1000 via UPI Payment
```

---

## ✔️ How Strategy Pattern is Applied

* `PaymentStrategy` → common interface
* `CreditCardPayment`, `UPIPayment`, `PayPalPayment` → interchangeable strategies
* `PaymentContext` → uses strategy (composition, not inheritance)
* Runtime selection via user input

---

## ✔️ Key Benefits

* ✅ Easy to add new payment methods
* ✅ No modification in existing code (Open/Closed Principle)
* ✅ Clean separation of logic

---

If you want, I can also convert this into a **short handwritten-style answer (for exams)** or add a **class diagram**.
