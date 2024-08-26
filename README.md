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
// Employee.java
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

// Payroll.java
public class Payroll {
    public void calculatePay(Employee employee) {
        // Logic...
    }
}
```

<b>2. Open/Closed Principle (OCP)</b> <br/>
<mark>An existing class cannot be modified but can be extended by inheritance.</mark> <br/>
<i>OCP Violation: Suppose you have an <b>AreaCalculator</b> class to calculate the area of ​​different shapes like rectangles and circles.</i>
```
// Rectangle.java
public class Rectangle {
    public double length;
    public double width;
}

// Circle.java
public class Circle {
    public double radius;
}

// AreaCalculator.java
public class AreaCalculator {
    public double calculateArea(Object shape) {
        double area = 0;
        if (shape instanceof Rectangle) {
            Rectangle rectangle = (Rectangle) shape;
            area = rectangle.length * rectangle.width;
        } else if (shape instanceof Circle) {
            Circle circle = (Circle) shape;
            area = Math.PI * circle.radius * circle.radius;
        }
        return area;
    }
}
```
<li><b>Problem:</b> If you want to add a new shape, say Triangle, you must change the calculateArea method in the AreaCalculator class, which violates OCP because the class is not "closed" for editing.</li>

<b>3. Liskov Substitution Principle (LSP)</b>

<b>4. Interface Segregation Principle (ISP)</b>

<b>5. Dependency Inversion Principle (DIP)</b>
