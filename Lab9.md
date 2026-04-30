Your earlier answer was on the right track, but let’s tighten it so it fully matches the question (intent + clear mapping to problem + diagram + working program).

---

# ✔️ Design Pattern: **Factory Method Pattern**

---

## 🔹 Intent

The **Factory Method Pattern** defines an interface for creating objects, but allows subclasses to decide which class to instantiate. It lets a class defer instantiation to subclasses.

👉 In this case:
Each franchise (Mumbai, Jaipur) will **create its own golgappas locally**, instead of depending on a central factory.

---

## 🔹 Mapping to Problem

* **Product** → Golgappa
* **Concrete Products** → MumbaiStyleGolgappa, JaipurStyleGolgappa
* **Creator (Factory)** → GolgappaFactory
* **Concrete Creators** → MumbaiFactory, JaipurFactory

✔️ Each franchise has its **own factory**, solving distance & quality issues.

---

## 🔹 Class Diagram (Textual UML)**

```
                <<interface>>
                  Golgappa
                      |
        -----------------------------
        |                           |
MumbaiStyleGolgappa     JaipurStyleGolgappa


            <<abstract>>
           GolgappaFactory
                 |
        ----------------------
        |                    |
  MumbaiFactory        JaipurFactory
```

---

## 🔹 Program (Java)

```java
// Product
interface Golgappa {
    void prepare();
}

// Concrete Products
class MumbaiStyleGolgappa implements Golgappa {
    public void prepare() {
        System.out.println("Preparing spicy Mumbai style Golgappa");
    }
}

class JaipurStyleGolgappa implements Golgappa {
    public void prepare() {
        System.out.println("Preparing tangy Jaipur style Golgappa");
    }
}

// Creator (Factory)
abstract class GolgappaFactory {
    abstract Golgappa createGolgappa();

    public void serveGolgappa() {
        Golgappa g = createGolgappa();
        g.prepare();
    }
}

// Concrete Factories
class MumbaiFactory extends GolgappaFactory {
    Golgappa createGolgappa() {
        return new MumbaiStyleGolgappa();
    }
}

class JaipurFactory extends GolgappaFactory {
    Golgappa createGolgappa() {
        return new JaipurStyleGolgappa();
    }
}

// Client
public class Main {
    public static void main(String[] args) {

        GolgappaFactory mumbaiFranchise = new MumbaiFactory();
        GolgappaFactory jaipurFranchise = new JaipurFactory();

        mumbaiFranchise.serveGolgappa();
        jaipurFranchise.serveGolgappa();
    }
}
```

---

## 🔹 Output

```
Preparing spicy Mumbai style Golgappa
Preparing tangy Jaipur style Golgappa
```

---

## 🔹 Why this solves the problem

* ❌ No centralized factory dependency
* ✅ Each franchise produces locally
* ✅ Easy to add new franchises (e.g., DelhiFactory)
* ✅ Maintains regional customization

---

This version directly addresses the **real-world scenario, pattern intent, structure, and implementation**, so it fully satisfies the question.
