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
*OCP Violation: Suppose you have an `AreaCalculator` class to calculate the area of different shapes like rectangles and circles.*

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
Problem: <span>If you want to add a new `shape`, say `Triangle`, you must change the `calculateArea` method in the `AreaCalculato`r class, which violates OCP because the class is not "closed" for editing.</span> <hr/>
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

<b>Benefits of the Open/Closed Principle (OCP) </b>

*Now, if you want to add a new shape, such as a `Triangle`, you only need to create a new `Triangle` class and implement the `Shape` interface, without changing any existing source code.*

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


**3. Liskov Substitution Principle (LSP)**
```java

```


**4. Interface Segregation Principle (ISP)**
<mark>Clients should not be forced to depend on interfaces they do not use.</mark> <br/>
*ISP Violation: A single interface that includes methods unrelated to all implementing classes.*
```java
// Worker.java
public interface Worker {
    void work();
    void eat();
}

// HumanWorker.java
public class HumanWorker implements Worker {
    @Override
    public void work() {
        // Human worker working
    }

    @Override
    public void eat() {
        // Human worker eating
    }
}

// RobotWorker.java
public class RobotWorker implements Worker {
    @Override
    public void work() {
        // Robot working
    }

    @Override
    public void eat() {
        // Robots don't eat, but still have to implement this method
    }
}
```

*ISP Compliance: Split the interface into multiple smaller, more specific interfaces.*
```java
// Workable.java
public interface Workable {
    void work();
}

// Eatable.java
public interface Eatable {
    void eat();
}

// HumanWorker.java
public class HumanWorker implements Workable, Eatable {
    @Override
    public void work() {
        // Human worker working
    }

    @Override
    public void eat() {
        // Human worker eating
    }
}

// RobotWorker.java
public class RobotWorker implements Workable {
    @Override
    public void work() {
        // Robot working
    }
}
```
**5. Dependency Inversion Principle (DIP)**
<mark>High-level modules should not depend on low-level modules. Both should depend on abstractions.</mark>
*DIP Violation: High-level module directly depends on a low-level module*
```java
public class LightBulb {
    public void turnOn() {
        // Logic to turn on the light bulb
    }

    public void turnOff() {
        // Logic to turn off the light bulb
    }
}

public class Switch {
    private LightBulb bulb;

    public Switch(LightBulb bulb) {
        this.bulb = bulb;
    }

    public void operate() {
        // Logic to operate the switch
        bulb.turnOn(); // Direct dependency on LightBulb
    }
}
```

*DIP Compliance: Depend on abstractions rather than concrete implementations.*
```java
public interface Switchable {
    void turnOn();
    void turnOff();
}

public class LightBulb implements Switchable {
    @Override
    public void turnOn() {
        // Logic to turn on the light bulb
    }

    @Override
    public void turnOff() {
        // Logic to turn off the light bulb
    }
}

public class Switch {
    private Switchable device;

    public Switch(Switchable device) {
        this.device = device;
    }

    public void operate() {
        // Logic to operate the switch
        device.turnOn(); // Depend on abstraction
    }
}
```
