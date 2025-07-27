#  Key Concepts of OOP

## 1. Encapsulation

Encapsulation is the bundling of data and methods that operate on that data within a single unit, or class.
It restricts direct access to some of an object's components, which can prevent the accidental modification of data.

### Goal of using Encapsulation

1. **Hide the internal implementation.**
1. **Expose only what's necessary.**

### Example in C#
```csharp
public class BankAccount
{
	private decimal balance;
	public void Deposit(decimal amount)
	{
		if (amount > 0)
		{
			balance += amount;
		}
	}
	public decimal GetBalance()
	{
		return balance;
	}
}
```



## 2. Inheritance

Inheritance allows a class to inherit properties and methods from another class, promoting code reuse and establishing a relationship between classes.

### Goal of using Inheritance
1. **Promote code reuse.**
1. **Establish a hierarchy.**

### Example in C#
```csharp

public class Animal
{
	public void Eat() { }
}

public class Dog : Animal
{
	public void Bark() { }
}

public class Cat : Animal
{
	public void Meow() { }
}
```

### Types of Inheritance

1. **Single Inheritance**: A class inherits from one base class.
	- Example: `Dog` inherits from `Animal`.
1. **Multiple Inheritance**: A class inherits from multiple base classes (not supported in C#).
	- Example: `class A : B, C` (not valid in C#).
1. **Multilevel Inheritance**: A class inherits from another derived class.
	- Example: `Dog` inherits from `Animal`, and `Puppy` inherits from `Dog`.
1. **Hierarchical Inheritance**: Multiple classes inherit from a single base class.
	- Example: `Dog` and `Cat` inherit from `Animal`.


### Access modifiers control which class members are inherited:

- **public**: Members are accessible from any class.
- **protected**: Members are accessible within the class and by derived classes.
- **private**: Members are accessible only within the class itself.
- **internal**: Members are accessible within the same assembly.


```csharp
class Animal
{
 private int age; // Not inherited
 protected string name; // Inherited, but not accessible outside the class hierarchy
 public void Communication() { Console.WriteLine("Comm..."); } // Inherited and accessible
} 

```



### base Keyword 

The `base` keyword is used to access members of the base class from a derived class. It can be used to call base class constructors or methods.
```csharp

public class Animal
{
	public void Speak() { Console.WriteLine("Animal speaks"); }
}
public class Dog : Animal
{
	public void Speak()
	{
		base.Speak(); // Calls the Speak method of the base class
		Console.WriteLine("Dog barks");
	}
}
public class Program
{
	public static void Main()
	{
		Dog dog = new Dog();
		dog.Speak(); // Output: Animal speaks \n Dog barks
	}
}
```





### Method Overriding and virtual/override Keywords

When a method in the base class is marked with the virtual keyword, it can be overridden in the
derived class using the override keyword. This allows the derived class to provide its own
implementation of the method.

```csharp
public class Animal
{
	public virtual void Speak()
	{
		Console.WriteLine("Animal speaks");
	}
}
public class Dog : Animal
{
	public override void Speak()
	{
		Console.WriteLine("Dog barks");
	}
}
public class Program
{
	public static void Main()
	{
		Animal animal = new Animal();
		animal.Speak(); // Output: Animal speaks
		Dog dog = new Dog();
		dog.Speak(); // Output: Dog barks
		Animal animalDog = new Dog();
		animalDog.Speak(); // Output: Dog barks (polymorphism)
	}
}
```

### Sealing Classes and Methods

A class can be sealed using the `sealed` keyword, which prevents it from being inherited. A method can also be sealed to prevent further overriding in derived classes.
```csharp
public class Animal
{
	public virtual void Speak()
	{
		Console.WriteLine("Animal speaks");
	}
}
public sealed class Dog : Animal
{
	public override void Speak()
	{
		Console.WriteLine("Dog barks");
	}
}
public class Cat : Animal
{
	// Cannot override Speak() here because Dog is sealed
	public override void Speak()
	{
		Console.WriteLine("Cat meows");
	}
}
public class Program
{
	public static void Main()
	{
		Animal animal = new Dog();
		animal.Speak(); // Output: Dog barks
	}
}
```


### Hiding Base Class Members

Sometimes, you may want to provide a new implementation in the derived class but not override
the base class method. In this case, you can use the new keyword to hide the base class member.

```csharp
public class Animal
{
	public void Speak()
	{
		Console.WriteLine("Animal speaks");
	}
}
public class Dog : Animal
{
	public new void Speak()
	{
		Console.WriteLine("Dog barks");
	}
}
public class Program
{
	public static void Main()
	{
		Animal animal = new Animal();
		animal.Speak(); // Output: Animal speaks
		Dog dog = new Dog();
		dog.Speak(); // Output: Dog barks
		Animal animalDog = new Dog();
		animalDog.Speak(); // Output: Animal speaks (base class method called)
	}
}
```


### Constructor Inheritance

When a derived class object is created, the base class constructor is called first, followed by the
derived class constructor. If the base class has a parameterized constructor, the derived class
must use the base keyword to pass arguments to it.

```csharp
public class Animal
{
	public Animal(string name)
	{
		Console.WriteLine($"Animal created: {name}");
	}
}
public class Dog : Animal
{
	public Dog(string name) : base(name)
	{
		Console.WriteLine($"Dog created: {name}");
	}
}
public class Program
{
	public static void Main()
	{
		Dog dog = new Dog("Buddy"); // Output: Animal created: Buddy \n Dog created: Buddy
	}
}
```
### Abstract Classes and Inheritance

An abstract class can provide some method implementations and force derived classes to
implement specific methods using abstract methods. Abstract methods do not have an
implementation in the base class and must be implemented in derived classes.

```csharp
public abstract class Animal
{
	public abstract void Speak(); // Abstract method with no implementation
	public void Eat() // Regular method with implementation
	{
		Console.WriteLine("Animal eats");
	}
}
public class Dog : Animal
{
	public override void Speak() // Implementing the abstract method
	{
		Console.WriteLine("Dog barks");
	}
}
public class Program
{
	public static void Main()
	{
		Dog dog = new Dog();
		dog.Speak(); // Output: Dog barks
		dog.Eat(); // Output: Animal eats
	}
}
```

## 3. Polymorphism 

Polymorphism allows objects of different classes to be treated as objects of a common base class.
It enables a single interface to represent different underlying forms (data types).

In C#, polymorphism is mainly achieved through method overriding, method overloading, and
interfaces. There are two types of polymorphism:

1. **Compile-time Polymorphism**: Achieved through method overloading and operator overloading.
1. **Run-time Polymorphism**: Achieved through method overriding using virtual and override keywords.

### Compile-time Polymorphism (Static Binding)

Compile-time polymorphism is achieved through method overloading and operator overloading.

#### Method Overloading
Method overloading allows multiple methods with the same name but different parameters (type, number, or order) to exist in the same class.
```csharp
public class MathOperations
{
	public int Add(int a, int b)
	{
		return a + b;
	}
	public double Add(double a, double b)
	{
		return a + b;
	}
	public int Add(int a, int b, int c)
	{
		return a + b + c;
	}
}
public class Program
{
	public static void Main()
	{
		MathOperations math = new MathOperations();
		Console.WriteLine(math.Add(2, 3)); // Output: 5
		Console.WriteLine(math.Add(2.5, 3.5)); // Output: 6.0
		Console.WriteLine(math.Add(1, 2, 3)); // Output: 6
	}
}
```

#### Operator Overloading

Operator overloading allows you to define custom behavior for operators (like +, -, *, etc.) for user-defined types (classes or structs).
```csharp
public class ComplexNumber
{
	public double Real { get; set; }
	public double Imaginary { get; set; }
	public ComplexNumber(double real, double imaginary)
	{
		Real = real;
		Imaginary = imaginary;
	}
	public static ComplexNumber operator +(ComplexNumber c1, ComplexNumber c2)
	{
		return new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary);
	}
}
public class Program
{
	public static void Main()
	{
		ComplexNumber c1 = new ComplexNumber(1, 2);
		ComplexNumber c2 = new ComplexNumber(3, 4);
		ComplexNumber result = c1 + c2; // Uses overloaded + operator
		Console.WriteLine($"Result: {result.Real} + {result.Imaginary}i"); // Output: Result: 4 + 6i
	}
}
```

### Run-time Polymorphism (Dynamic Binding)
Run-time polymorphism occurs when the method that needs to be invoked is determined during
runtime rather than compile time. It is achieved through:
1. Method overriding using virtual and override keywords
	- Method overriding occurs when a derived class has a method with the same name and signature
as in the base class. The base class method must be marked with the virtual keyword, and the
derived class overrides this method using the override keyword.

	- ### Example of Method Overriding
```csharp
			// Base class representing a general bank account
class BankAccount
{
 protected double balance;
 public BankAccount(double initialBalance)
 {
 balance = initialBalance;
 }
 // Virtual method that can be overridden in derived classes
 public virtual void Withdraw(double amount)
 {
 balance -= amount;
 Console.WriteLine($"{amount:C} withdrawn. New balance: {balance:C}");
 }
 public void ShowBalance()
 { Console.WriteLine($"Balance: {balance:C}"); }
}
// Derived class representing a savings account with withdrawal limits
class SavingsAccount : BankAccount
{
 public SavingsAccount(double initialBalance) : base(initialBalance) { }
 // Override the Withdraw method to implement specific logic for savings accounts
 public override void Withdraw(double amount)
 {
 if (amount > balance)
 {
 Console.WriteLine("Insufficient funds in Savings Account.");
 }
 else
 {
 base.Withdraw(amount); // Use the base class Withdraw method
 }
 }
}
// Derived class representing a current account with overdraft limit
class CurrentAccount : BankAccount
{
 private double overdraftLimit;
 public CurrentAccount(double initialBalance, double overdraftLimit) : base(initialBalance)
 {
 this.overdraftLimit = overdraftLimit;
 }
 // Override the Withdraw method to allow overdraft
 public override void Withdraw(double amount)
 {
 if (amount > balance + overdraftLimit)
 {
 Console.WriteLine("Withdrawal exceeds overdraft limit.");
 }
 else
 {
 base.Withdraw(amount);
 }
 }
}
class Program
{
 static void Main()
 {
 BankAccount savings = new SavingsAccount(1000);
 BankAccount current = new CurrentAccount(1000, 500);
 savings.Withdraw(1500); // Output: Insufficient funds in Savings Account.
 current.Withdraw(1500); // Output: $1,500.00 withdrawn. New balance: $-500.00
 }
}
 ```


2. Interfaces and their implementations



