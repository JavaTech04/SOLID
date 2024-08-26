# SOLID: The First 5 Principles of Object-Oriented Design

**1. Single Responsibility Principle (SRP)**  
<mark>Each class should only have one responsibility.</mark>  
*SRP Violation: This class is responsible for managing employee information and calculating salaries.*

```java
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
```java
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

**2. Open/Closed Principle (OCP)**  
<mark>An existing class cannot be modified but can be extended by inheritance.</mark>  
*OCP Violation: Suppose you have an **AreaCalculator** class to calculate the area of different shapes like rectangles and circles.*

```java
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
Problem: <span>If you want to add a new shape, say Triangle, you must change the calculateArea method in the AreaCalculator class, which violates OCP because the class is not "closed" for editing.</span> <br/>
*OCP Compliance: To adhere to the OCP rule, you can separate the logic into separate classes, using a Shape interface that all shapes will implement.*
```java
// Shape.java
public interface Shape {
    double calculateArea();
}

// Rectangle.java
public class Rectangle implements Shape {
    private double length;
    private double width;

    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    @Override
    public double calculateArea() {
        return length * width;
    }
}

// Circle.java
public class Circle implements Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

// AreaCalculator.java
public class AreaCalculator {
    public double calculateTotalArea(List<Shape> shapes) {
        double totalArea = 0;
        for (Shape shape : shapes) {
            totalArea += shape.calculateArea();
        }
        return totalArea;
    }
}

```

## Benefits of the Open/Closed Principle (OCP)

### Open for Extension
Now, if you want to add a new shape, such as a `Triangle`, you only need to create a new `Triangle` class and implement the `Shape` interface, without changing any existing source code.

```java
public class Triangle implements Shape {
    private double base;
    private double height;

    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    @Override
    public double calculateArea() {
        return 0.5 * base * height;
    }
}
```

<b>3. Liskov Substitution Principle (LSP)</b>

<b>4. Interface Segregation Principle (ISP)</b>

<b>5. Dependency Inversion Principle (DIP)</b>
