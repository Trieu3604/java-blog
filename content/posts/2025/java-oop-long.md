---
title: "Lập trình Hướng Đối Tượng trong Java – Hành trình từ cơ bản đến nâng cao"
date: 2025-10-01
slug: /java-oop-hanh-trinh/
description: Tìm hiểu chi tiết về lập trình hướng đối tượng (OOP) trong Java với 4 nguyên lý cơ bản
image: images/javaoop.jpg
caption: Photo by 
draft: false
tags: ["Java", "OOP", "Lập trình"]
categories: ["Lập trình"]
---

## Giới thiệu

Nếu bạn muốn thành thạo Java, việc hiểu rõ **Lập trình Hướng Đối Tượng (OOP - Object-Oriented Programming)** là điều bắt buộc. OOP không chỉ là một kỹ thuật lập trình, mà là một **tư duy** giúp bạn thiết kế và xây dựng phần mềm một cách có tổ chức, dễ bảo trì và mở rộng.

Trong bài viết này, chúng ta sẽ đi từ những khái niệm cơ bản nhất đến các ví dụ thực tế, giúp bạn nắm vững 4 trụ cột của OOP trong Java.

## OOP là gì?

**Object-Oriented Programming (OOP)** là mô hình lập trình dựa trên khái niệm **"đối tượng"** (objects). Thay vì viết code theo kiểu tuần tự (procedural), OOP tổ chức code xung quanh các đối tượng có:
- **Thuộc tính** (attributes/properties): Dữ liệu của đối tượng
- **Phương thức** (methods): Hành vi của đối tượng

### So sánh Procedural vs OOP

**Procedural Programming:**
```java
// Dữ liệu và functions tách biệt
String studentName = "John";
int studentAge = 20;

void printStudent(String name, int age) {
    System.out.println(name + " - " + age);
}
```

**Object-Oriented Programming:**
```java
// Dữ liệu và methods gom trong object
class Student {
    // Thuộc tính
    String name;
    int age;
    
    // Constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Phương thức
    void printInfo() {
        System.out.println(name + " - " + age);
    }
}

// Sử dụng
Student student = new Student("John", 20);
student.printInfo();
```

## 4 trụ cột của OOP

### 1. Encapsulation (Đóng gói) 📦

**Định nghĩa:** Encapsulation là việc ẩn giấu dữ liệu bên trong và chỉ cho phép truy cập thông qua các phương thức công khai.

**Tại sao cần Encapsulation?**
- ✅ Bảo vệ dữ liệu khỏi truy cập trái phép
- ✅ Kiểm soát cách dữ liệu được thay đổi
- ✅ Dễ bảo trì và thay đổi implementation
- ✅ Tăng tính bảo mật

**Ví dụ thực tế:**

```java
// ❌ BAD - Không có encapsulation
class BankAccount {
    public double balance; // Ai cũng có thể thay đổi!
}

// Sử dụng
BankAccount account = new BankAccount();
account.balance = 1000000; // Có thể gán bất kỳ giá trị nào!
account.balance = -500;    // Số âm? Không kiểm soát được!

// ✅ GOOD - Có encapsulation
class BankAccount {
    private double balance; // Private - chỉ class này truy cập được
    
    // Constructor
    public BankAccount(double initialBalance) {
        if (initialBalance >= 0) {
            this.balance = initialBalance;
        } else {
            this.balance = 0;
        }
    }
    
    // Getter
    public double getBalance() {
        return balance;
    }
    
    // Deposit với validation
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Nạp thành công: " + amount);
        } else {
            System.out.println("Số tiền phải > 0");
        }
    }
    
    // Withdraw với validation
    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Rút thành công: " + amount);
            return true;
        } else {
            System.out.println("Không đủ tiền hoặc số tiền không hợp lệ");
            return false;
        }
    }
}

// Sử dụng
BankAccount account = new BankAccount(1000000);
account.deposit(500000);      // OK
account.withdraw(200000);     // OK
account.withdraw(2000000);    // Fail - không đủ tiền
// account.balance = -500;    // ❌ Compile error - không thể truy cập trực tiếp
```

**Access Modifiers trong Java:**

| Modifier | Class | Package | Subclass | World |
|----------|-------|---------|----------|-------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| `default` | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

### 2. Inheritance (Kế thừa) 🧬

**Định nghĩa:** Inheritance cho phép một class (class con) kế thừa thuộc tính và phương thức từ class khác (class cha).

**Lợi ích:**
- ✅ Tái sử dụng code
- ✅ Giảm duplicate code
- ✅ Tạo hierarchy rõ ràng
- ✅ Dễ mở rộng

**Ví dụ thực tế:**

```java
// Class cha (Parent/Super class)
class Animal {
    protected String name;
    protected int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void eat() {
        System.out.println(name + " đang ăn");
    }
    
    public void sleep() {
        System.out.println(name + " đang ngủ");
    }
    
    public void makeSound() {
        System.out.println("Some sound...");
    }
}

// Class con (Child/Sub class)
class Dog extends Animal {
    private String breed;
    
    public Dog(String name, int age, String breed) {
        super(name, age); // Gọi constructor của class cha
        this.breed = breed;
    }
    
    // Override method của class cha
    @Override
    public void makeSound() {
        System.out.println(name + " kêu: Gâu gâu!");
    }
    
    // Method riêng của Dog
    public void fetch() {
        System.out.println(name + " đang đuổi theo bóng");
    }
}

class Cat extends Animal {
    private boolean isIndoor;
    
    public Cat(String name, int age, boolean isIndoor) {
        super(name, age);
        this.isIndoor = isIndoor;
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " kêu: Meo meo!");
    }
    
    public void scratch() {
        System.out.println(name + " đang cào");
    }
}

// Sử dụng
Dog dog = new Dog("Buddy", 3, "Golden Retriever");
dog.eat();        // Kế thừa từ Animal
dog.sleep();      // Kế thừa từ Animal
dog.makeSound();  // Override - "Buddy kêu: Gâu gâu!"
dog.fetch();      // Method riêng của Dog

Cat cat = new Cat("Whiskers", 2, true);
cat.makeSound();  // "Whiskers kêu: Meo meo!"
cat.scratch();
```

**Keyword `super`:**

```java
class Vehicle {
    protected String brand;
    
    public Vehicle(String brand) {
        this.brand = brand;
        System.out.println("Vehicle constructor called");
    }
    
    public void start() {
        System.out.println("Vehicle starting...");
    }
}

class Car extends Vehicle {
    private int doors;
    
    public Car(String brand, int doors) {
        super(brand); // Gọi constructor của Vehicle
        this.doors = doors;
        System.out.println("Car constructor called");
    }
    
    @Override
    public void start() {
        super.start(); // Gọi method của class cha
        System.out.println("Car engine starting...");
    }
}
```

### 3. Polymorphism (Đa hình) 🎭

**Định nghĩa:** Polymorphism cho phép một object có thể có nhiều hình thái khác nhau. Cùng một method có thể hoạt động khác nhau tùy object.

**Có 2 loại:**
1. **Compile-time Polymorphism** (Method Overloading)
2. **Runtime Polymorphism** (Method Overriding)

#### Method Overloading (Nạp chồng)

```java
class Calculator {
    // Cùng tên method, khác parameters
    
    public int add(int a, int b) {
        return a + b;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
    
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    public String add(String a, String b) {
        return a + b;
    }
}

// Sử dụng
Calculator calc = new Calculator();
System.out.println(calc.add(5, 3));           // 8 (int)
System.out.println(calc.add(5.5, 3.2));       // 8.7 (double)
System.out.println(calc.add(1, 2, 3));        // 6
System.out.println(calc.add("Hello", "World")); // HelloWorld
```

#### Method Overriding (Ghi đè)

```java
class Shape {
    public void draw() {
        System.out.println("Vẽ hình");
    }
    
    public double calculateArea() {
        return 0;
    }
}

class Circle extends Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public void draw() {
        System.out.println("Vẽ hình tròn");
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    private double width, height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    @Override
    public void draw() {
        System.out.println("Vẽ hình chữ nhật");
    }
    
    @Override
    public double calculateArea() {
        return width * height;
    }
}

// Runtime Polymorphism
Shape shape1 = new Circle(5);
Shape shape2 = new Rectangle(4, 6);

shape1.draw();  // "Vẽ hình tròn"
shape2.draw();  // "Vẽ hình chữ nhật"

System.out.println("Area: " + shape1.calculateArea()); // 78.54
System.out.println("Area: " + shape2.calculateArea()); // 24
```

### 4. Abstraction (Trừu tượng) 🎨

**Định nghĩa:** Abstraction là việc ẩn giấu các chi tiết phức tạp và chỉ hiển thị những tính năng cần thiết.

**Cách implement:**
1. **Abstract Class** - Class trừu tượng
2. **Interface** - Giao diện

#### Abstract Class

```java
// Abstract class - không thể tạo object trực tiếp
abstract class Vehicle {
    protected String brand;
    
    public Vehicle(String brand) {
        this.brand = brand;
    }
    
    // Abstract method - không có implementation
    abstract void start();
    abstract void stop();
    
    // Concrete method - có implementation
    public void displayBrand() {
        System.out.println("Brand: " + brand);
    }
}

class Car extends Vehicle {
    public Car(String brand) {
        super(brand);
    }
    
    @Override
    void start() {
        System.out.println(brand + " car is starting with key");
    }
    
    @Override
    void stop() {
        System.out.println(brand + " car stopped");
    }
}

class Motorcycle extends Vehicle {
    public Motorcycle(String brand) {
        super(brand);
    }
    
    @Override
    void start() {
        System.out.println(brand + " motorcycle is starting with kick");
    }
    
    @Override
    void stop() {
        System.out.println(brand + " motorcycle stopped");
    }
}

// Sử dụng
// Vehicle vehicle = new Vehicle("Toyota"); // ❌ Error - không thể tạo object
Vehicle car = new Car("Toyota");
car.start();         // "Toyota car is starting with key"
car.displayBrand();  // "Brand: Toyota"
```

#### Interface

```java
// Interface - 100% abstraction
interface Drawable {
    // Tất cả methods đều abstract (implicit)
    void draw();
    void resize(double scale);
}

interface Colorable {
    void setColor(String color);
    String getColor();
}

// Class implement nhiều interfaces
class Square implements Drawable, Colorable {
    private double size;
    private String color;
    
    public Square(double size) {
        this.size = size;
        this.color = "Black";
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing a " + color + " square");
    }
    
    @Override
    public void resize(double scale) {
        size *= scale;
        System.out.println("Resized to: " + size);
    }
    
    @Override
    public void setColor(String color) {
        this.color = color;
    }
    
    @Override
    public String getColor() {
        return color;
    }
}

// Sử dụng
Square square = new Square(10);
square.setColor("Red");
square.draw();      // "Drawing a Red square"
square.resize(2);   // "Resized to: 20.0"
```

## Ví dụ tổng hợp - Hệ thống quản lý nhân viên

```java
// Abstract class
abstract class Employee {
    protected String name;
    protected String id;
    protected double baseSalary;
    
    public Employee(String name, String id, double baseSalary) {
        this.name = name;
        this.id = id;
        this.baseSalary = baseSalary;
    }
    
    // Abstract method
    abstract double calculateSalary();
    
    // Concrete method
    public void displayInfo() {
        System.out.println("ID: " + id);
        System.out.println("Name: " + name);
        System.out.println("Salary: " + calculateSalary());
    }
}

// Inheritance
class FullTimeEmployee extends Employee {
    private double bonus;
    
    public FullTimeEmployee(String name, String id, double baseSalary, double bonus) {
        super(name, id, baseSalary);
        this.bonus = bonus;
    }
    
    @Override
    double calculateSalary() {
        return baseSalary + bonus;
    }
}

class PartTimeEmployee extends Employee {
    private int hoursWorked;
    private double hourlyRate;
    
    public PartTimeEmployee(String name, String id, int hoursWorked, double hourlyRate) {
        super(name, id, 0);
        this.hoursWorked = hoursWorked;
        this.hourlyRate = hourlyRate;
    }
    
    @Override
    double calculateSalary() {
        return hoursWorked * hourlyRate;
    }
}

// Sử dụng Polymorphism
public class Main {
    public static void main(String[] args) {
        Employee[] employees = new Employee[3];
        
        employees[0] = new FullTimeEmployee("John", "FT001", 20000000, 5000000);
        employees[1] = new PartTimeEmployee("Jane", "PT001", 100, 50000);
        employees[2] = new FullTimeEmployee("Bob", "FT002", 15000000, 3000000);
        
        // Polymorphism - cùng method, khác implementation
        for (Employee emp : employees) {
            emp.displayInfo();
            System.out.println("---");
        }
    }
}
```

## Best Practices

### 1. Favor Composition over Inheritance

```java
// ❌ Inheritance overuse
class Rectangle extends Shape, Drawable, Colorable { }

// ✅ Composition
class Rectangle {
    private Shape shape;
    private Color color;
    
    public void draw() {
        shape.draw();
    }
}
```

### 2. Program to Interface, not Implementation

```java
// ✅ GOOD
List<String> list = new ArrayList<>();

// ❌ BAD
ArrayList<String> list = new ArrayList<>();
```

### 3. Encapsulate what varies

```java
class Product {
    private double price;
    
    // Có thể thay đổi logic discount dễ dàng
    public double calculateDiscount() {
        return price * 0.1;
    }
}
```

## Kết luận

4 trụ cột của OOP trong Java:

1. **Encapsulation** 📦 - Bảo vệ dữ liệu với private/public
2. **Inheritance** 🧬 - Tái sử dụng code với extends
3. **Polymorphism** 🎭 - Một interface, nhiều implementations
4. **Abstraction** 🎨 - Ẩn complexity với abstract/interface

**Lợi ích của OOP:**
- ✅ Code dễ bảo trì và mở rộng
- ✅ Tái sử dụng code tốt hơn
- ✅ Dễ debug và test
- ✅ Modeling gần với thế giới thực

Để thành thạo OOP, hãy:
1. **Thực hành nhiều** - Làm projects thực tế
2. **Đọc code người khác** - Học cách thiết kế
3. **Học Design Patterns** - Singleton, Factory, Observer
4. **Refactor code** - Cải thiện design liên tục

Chúc bạn thành công trên hành trình chinh phục OOP trong Java! 🚀☕

---

**Bạn có thắc mắc về OOP không?** Hãy comment bên dưới nhé! 💬

## Ứng dụng thực tế của OOP
**Phát triển phần mềm lớn:** dễ bảo trì, mở rộng.

**Lập trình Android:** Java là ngôn ngữ chính trước đây.

**Hệ thống doanh nghiệp:** ERP, CRM đều áp dụng OOP.

## Kết luận

OOP là nền tảng giúp bạn trở thành lập trình viên Java giỏi.
Hãy luyện tập thật nhiều bằng cách viết các lớp, kế thừa và áp dụng 4 nguyên lý trên.
```
“Hiểu OOP là bạn đã đi được nửa chặng đường học Java.”
```