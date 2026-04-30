### **Short Question**

Design a word processor with `Document` (high-level) and `Page` (low-level) such that `Page` does not call `Document`, and `Document` triggers page re-rendering.

---

## **Solution**

### **a) Design Principle**

**Dependency Inversion Principle (DIP)**
*High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions.*

---

### **b) Class Diagram (Detailed)**

```
+----------------------+
|     <<interface>>    |
|       Renderer       |
+----------------------+
| + render() : void    |
+----------^-----------+
           |
           |
+----------------------+
|        Page          |
+----------------------+
| - content : String   |
+----------------------+
| + Page(content)      |
| + render() : void    |
+----------------------+


+-----------------------------------+
|             Document              |
+-----------------------------------+
| - pages : List<Renderer>          |
+-----------------------------------+
| + addPage(r : Renderer) : void    |
| + updateDocument() : void         |
+-----------------------------------+

Relationship:
Document "has-a" List of Renderer (Aggregation)
Page "implements" Renderer
```

---

### **c) Implementation (Java)**

```java
import java.util.*;

// Abstraction
interface Renderer {
    void render();
}

// Low-level module
class Page implements Renderer {
    private String content;

    Page(String content) {
        this.content = content;
    }

    public void render() {
        System.out.println("Rendering page: " + content);
    }
}

// High-level module
class Document {
    private List<Renderer> pages = new ArrayList<>();

    public void addPage(Renderer page) {
        pages.add(page);
    }

    public void updateDocument() {
        System.out.println("Document updated. Re-rendering pages...");
        for (Renderer p : pages) {
            p.render();
        }
    }
}

// Main class
public class Main {
    public static void main(String[] args) {
        Document doc = new Document();

        doc.addPage(new Page("Page 1 Content"));
        doc.addPage(new Page("Page 2 Content"));

        doc.updateDocument();
    }
}
```

---

### **Output**

```
Document updated. Re-rendering pages...
Rendering page: Page 1 Content
Rendering page: Page 2 Content
```

---

### **Summary**

The improved diagram clearly shows abstraction (`Renderer`), implementation (`Page`), and dependency (`Document → Renderer`). This ensures loose coupling and correct dependency direction as per DIP.
