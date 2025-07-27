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
