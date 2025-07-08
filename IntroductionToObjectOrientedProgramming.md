# Object Oriented Programming


## What is Object Oriented Programming?

Object Oriented Programming (OOP) is a programming paradigm that uses **objects** to represent **data** and **methods**.
It allows for the creation of **reusable code**, **encapsulation of data**, 
and **inheritance of properties** and **methods from other classes**.

![OOP Concept](./image/OOP-Concepts.jpg)




## Key Concepts of OOP

### 1. Classes and Objects
- **Class**: A blueprint for creating objects. It defines properties and methods that the objects created from the class will have.
- **Object**: An instance of a class. It contains data and methods defined by the class.

### 2. Encapsulation

- Encapsulation is the bundling of data and methods that operate on that data within a single unit (class).
- It restricts direct access to some of an object's components, which can prevent the accidental modification of data.
- Encapsulation is achieved using access modifiers:
  - **Public**: Members are accessible from outside the class.
  - **Private**: Members are accessible only within the class.
  - **Protected**: Members are accessible within the class and by derived classes.

### 3. Inheritance
- Inheritance allows a class (child class) to inherit properties and methods from another class (parent class).
- It promotes code reusability and establishes a relationship between classes.

### 4. Polymorphism
- Polymorphism allows methods to do different things based on the object it is acting upon.
- It can be achieved through:
  - **Method Overloading**: Multiple methods with the same name but different parameters.

### 5. Abstraction
- Abstraction is the concept of hiding complex implementation details and showing only the essential features of an object.
- It can be achieved using abstract classes and interfaces.


## Benefits of Object-Oriented Programming:

- **Modularity**: Code is organized into classes, making it easier to manage and understand.
- **Reusability**: Classes can be reused across different programs, reducing redundancy.
- **Maintainability**: Changes in one part of the code can be made with minimal impact on other parts.
- **Scalability**: OOP allows for the creation of complex systems that can be easily extended.
- **Flexibility**: OOP allows for the creation of systems that can adapt to changing requirements.

## Create class and object :

```csharp
// Defining a class named Car
public class Car
{
	// Properties
	public string Make { get; set; } // Make of the car : get and set -> allows reading and writing
	public string Model { get; set; } 
	public int Year { get; set; }


	// Constructor initializes the properties
	public Car(string make, string model, int year) 
	{
		Make = make;  // Assigning values to properties
		Model = model;
		Year = year;
	}


	// Method
	public void DisplayInfo() // Method to display car information
	{
		Console.WriteLine($"Car: {Year} {Make} {Model}");
	}
}

// Creating an object of the Car class
// Creating an instance of the Car class with specific values
Car myCar = new Car("Toyota", "Corolla", 2020); 

// Calling the method

myCar.DisplayInfo(); // Output: Car: 2020 Toyota Corolla

```

## Class Constructors

A **constructor** is a special method that is called when an object of a class is created. It initializes the object's properties.

### Types of Constructors:
1. **Default Constructor**: A constructor that does not take any parameters. It initializes properties with default values.

**Example of Default Constructor:**
```csharp
public class Car
{
	public string Make { get; set; }
	public string Model { get; set; }
	public int Year { get; set; }
	// Default constructor
	public Car()
	{
		Make = "Unknown";
		Model = "Unknown";
		Year = 0;
	}
	public void DisplayInfo()
	{
		Console.WriteLine($"Car: {Year} {Make} {Model}");
	}
}

// Creating an object using the default constructor
Car myDefaultCar = new Car();
myDefaultCar.DisplayInfo(); // Output: Car: 0 Unknown Unknown
```
2. **Parameterized Constructor**: A constructor that takes parameters to initialize properties with specific values.

**Example of Parameterized Constructor:**
```csharp
public class Car
{
	public string Make { get; set; }
	public string Model { get; set; }
	public int Year { get; set; }
	// Parameterized constructor
	public Car(string make, string model, int year)
	{
		Make = make;
		Model = model;
		Year = year;
	}
	public void DisplayInfo()
	{
		Console.WriteLine($"Car: {Year} {Make} {Model}");
	}
}

// Creating an object using the parameterized constructor

Car myCar = new Car("Toyota", "Corolla", 2020);

myCar.DisplayInfo(); // Output: Car: 2020 Toyota Corolla
```

3. **Copy Constructor**: A constructor that creates a new object as a copy of an existing object.

**Example of Copy Constructor:**
```csharp

public class Car
{
	public string Make { get; set; }
	public string Model { get; set; }
	public int Year { get; set; }
	// Copy constructor
	public Car(Car existingCar)
	{
		Make = existingCar.Make;
		Model = existingCar.Model;
		Year = existingCar.Year;
	}
	public void DisplayInfo()
	{
		Console.WriteLine($"Car: {Year} {Make} {Model}");
	}
}

// Creating an object using the copy constructor

Car originalCar = new Car("Honda", "Civic", 2019);
Car copiedCar = new Car(originalCar);

copiedCar.DisplayInfo(); // Output: Car: 2019 Honda Civic
```

4. **Static Constructor**: A constructor that initializes static members of the class. It is called once, before any static members are accessed or any objects are created.

**Example of Static Constructor:**
```csharp

public class Car
{
	public static int TotalCars { get; private set; } // Static property to keep track of total cars
	public string Make { get; set; }
	public string Model { get; set; }
	public int Year { get; set; }
	// Static constructor
	static Car()
	{
		TotalCars = 0; // Initialize static property
	}
	// Parameterized constructor
	public Car(string make, string model, int year)
	{
		Make = make;
		Model = model;
		Year = year;
		TotalCars++; // Increment total cars when a new car is created
	}
	public void DisplayInfo()
	{
		Console.WriteLine($"Car: {Year} {Make} {Model}");
	}
}

// Creating objects of the Car class

Car car1 = new Car("Ford", "Mustang", 2021);
Car car2 = new Car("Chevrolet", "Camaro", 2022);

car1.DisplayInfo(); // Output: Car: 2021 Ford Mustang
car2.DisplayInfo(); // Output: Car: 2022 Chevrolet Camaro

Console.WriteLine($"Total Cars Created: {Car.TotalCars}"); // Output: Total Cars Created: 2
```

