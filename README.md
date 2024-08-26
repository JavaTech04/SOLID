# SOLID: The First 5 Principles of Object-Oriented Design

<b>1. Single Responsibility Principle (SRP)</b> <br/>
<mark> Each class should only have one responsibility.</mark> <br/>
<i>SRP Violation: This class is responsible for managing employee information and calculating salaries.</i>
```
public class Employee {
    private String name;
    private String position;
    
    public void calculatePay() {
        // Logic...
    }
    
    public String getName() {
        return name;
    }
    
    public String getPosition() {
        return position;
    }
}
```

<i>SRP Compliance: Separate payroll work into a separate layer.</i>
```
public class Employee {
    private String name;
    private String position;

    public String getName() {
        return name;
    }

    public String getPosition() {
        return position;
    }
}

public class Payroll {
    public void calculatePay(Employee employee) {
        // Logic...
    }
}
```

<b>2. Open/Closed Principle (OCP)</b>
<mark>An existing class cannot be modified but can be extended by inheritance.</mark> <br/>
<i>OCP Violation: Suppose you have an <b>AreaCalculator</b> class to calculate the area of ​​different shapes like rectangles and circles.</i>

<b>3. Liskov Substitution Principle (LSP)</b>

<b>4. Interface Segregation Principle (ISP)</b>

<b>5. Dependency Inversion Principle (DIP)</b>
