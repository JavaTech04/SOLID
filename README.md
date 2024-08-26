# SOLID: The First 5 Principles of Object-Oriented Design

<b>1. Single Responsibility Principle (SRP)</b> <br/>
<mark> Each class should only have one responsibility.</mark> <br/>
<i>SRP Violation: This class is responsible for managing employee information and calculating salaries.</i>
```
public class Employee {
    private String name;
    private String position;
    
    public void calculatePay() {
        // Logic tính lương
    }
    
    public String getName() {
        return name;
    }
    
    public String getPosition() {
        return position;
    }
}
```

<b>2. Open/Closed Principle (OCP)</b>

<b>3. Liskov Substitution Principle (LSP)</b>

<b>4. Interface Segregation Principle (ISP)</b>

<b>5. Dependency Inversion Principle (DIP)</b>
