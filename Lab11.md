### **Short Question**

Design a payment processing system using the **Strategy Design Pattern** that supports Credit Card, UPI, and PayPal, allowing runtime selection of payment method.

---

## **Solution**

### **a) Intent (Strategy Pattern)**

Define a family of algorithms, encapsulate each one, and make them interchangeable so that the algorithm can vary independently from the client.

---

### **b) Class Diagram (Detailed)**

```id="stp983"
          +-----------------------------+
          |     <<interface>>           |
          |     PaymentStrategy         |
          +-----------------------------+
          | + processPayment(amount)    |
          +-------------^---------------+
                        |
      -----------------------------------------
      |                  |                    |
+----------------+ +----------------+ +------------------+
| CreditCardPay  | |   UPIPayment   | |  PayPalPayment   |
+----------------+ +----------------+ +------------------+
| +processPayment| | +processPayment| | +processPayment  |
+----------------+ +----------------+ +------------------+


            +------------------------------+
            |       PaymentContext         |
            +------------------------------+
            | - strategy: PaymentStrategy  |
            +------------------------------+
            | + setStrategy(s)             |
            | + pay(amount)                |
            +------------------------------+

Relationship:
PaymentContext "has-a" PaymentStrategy
Concrete strategies "implement" PaymentStrategy
```

---

### **c) Implementation (Java)**

```java id="pay873"
import java.util.Scanner;

// Strategy Interface
interface PaymentStrategy {
    void processPayment(int amount);
}

// Concrete Strategies
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

// Context Class
class PaymentContext {
    private PaymentStrategy strategy;

    public void setStrategy(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    public void pay(int amount) {
        strategy.processPayment(amount);
    }
}

// Main Class
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        PaymentContext context = new PaymentContext();

        System.out.print("Enter amount: ");
        int amount = sc.nextInt();

        System.out.println("Select Payment Method:");
        System.out.println("1. Credit Card  2. UPI  3. PayPal");

        int choice = sc.nextInt();

        switch (choice) {
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

### **Output (Sample Run)**

```id="out992"
Enter amount: 1000
Select Payment Method:
1. Credit Card  2. UPI  3. PayPal
Input: 2
Processing Rs.1000 via UPI Payment
```

---

### **Brief Explanation**

* `PaymentStrategy` defines a common interface.
* Each payment method implements its own strategy.
* `PaymentContext` uses a strategy but is independent of its implementation.
* Strategy can be changed at runtime → ensures flexibility and loose coupling.

---

### **Summary**

The Strategy Pattern cleanly separates payment algorithms and allows dynamic switching, making the system scalable and maintainable.
