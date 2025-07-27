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






