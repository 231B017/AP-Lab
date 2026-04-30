### **Short Question**

Design a system for Golgappa Stalls where each franchise (Mumbai, Jaipur) produces its own regional-style panipuri using the **Factory Method Pattern**, instead of relying on a central factory.

---

## **Solution**

### **Intent (Factory Method Pattern)**

Define an interface for creating an object, but let subclasses decide which class to instantiate. This allows each franchise to produce its own style of golgappa independently.

---

### **Class Diagram (Textual)**

```
          Golgappa (Product - Interface)
                ↑
   -----------------------------
   |                           |
MumbaiGolgappa        JaipurGolgappa

        GolgappaFactory (Creator - Abstract)
                  ↑
     --------------------------------
     |                              |
MumbaiFactory              JaipurFactory
```

---

### **Program (Java Example)**

```java
// Product Interface
interface Golgappa {
    void prepare();
}

// Concrete Products
class MumbaiGolgappa implements Golgappa {
    public void prepare() {
        System.out.println("Preparing spicy Mumbai style Golgappa");
    }
}

class JaipurGolgappa implements Golgappa {
    public void prepare() {
        System.out.println("Preparing sweet Jaipur style Golgappa");
    }
}

// Creator Abstract Class
abstract class GolgappaFactory {
    abstract Golgappa createGolgappa();

    public void serve() {
        Golgappa g = createGolgappa();
        g.prepare();
    }
}

// Concrete Factories
class MumbaiFactory extends GolgappaFactory {
    Golgappa createGolgappa() {
        return new MumbaiGolgappa();
    }
}

class JaipurFactory extends GolgappaFactory {
    Golgappa createGolgappa() {
        return new JaipurGolgappa();
    }
}

// Main Class
public class Main {
    public static void main(String[] args) {
        GolgappaFactory mumbai = new MumbaiFactory();
        GolgappaFactory jaipur = new JaipurFactory();

        mumbai.serve();
        jaipur.serve();
    }
}
```

---

### **Output**

```
Preparing spicy Mumbai style Golgappa
Preparing sweet Jaipur style Golgappa
```

---

### **Summary**

Each franchise now has its own factory, ensuring regional customization and eliminating dependency on a central factory—perfect use of the Factory Method Pattern.
