## ✔️ a) Design Principle

**Dependency Inversion Principle (DIP)**

**Complete Statement:**
High-level modules should not depend on low-level modules. Both should depend on abstractions.
Abstractions should not depend on details; details should depend on abstractions.

👉 Here:

* `Document` (high-level) should **not directly depend on Page implementation**
* `Page` should not call `Document`
* Both interact via an **abstraction (interface)**

---

## ✔️ b) Class Diagram (Textual UML)

```id="klm921"
        <<interface>>
          Page
            ^
            |
      -----------------
      |               |
  TextPage      ImagePage


          Document
            |
      uses (has list of)
            |
          Page
```

---

## ✔️ c) Implementation (Java)

```java id="abc482"
import java.util.*;

// Abstraction
interface Page {
    void render();
}

// Concrete Pages
class TextPage implements Page {
    public void render() {
        System.out.println("Rendering Text Page");
    }
}

class ImagePage implements Page {
    public void render() {
        System.out.println("Rendering Image Page");
    }
}

// High-level module
class Document {
    private List<Page> pages = new ArrayList<>();

    public void addPage(Page page) {
        pages.add(page);
    }

    // When document changes, it tells pages to re-render
    public void renderDocument() {
        System.out.println("Document changed. Re-rendering all pages...");
        for (Page p : pages) {
            p.render();
        }
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        Document doc = new Document();

        doc.addPage(new TextPage());
        doc.addPage(new ImagePage());

        doc.renderDocument();
    }
}
```

---

## ✔️ Output

```id="out562"
Document changed. Re-rendering all pages...
Rendering Text Page
Rendering Image Page
```

---

## ✔️ Key Points

* ❌ `Page` does NOT call `Document`
* ✅ `Document` controls updates
* ✅ Loose coupling via interface
* ✅ Easy to extend (new Page types without changing Document)
