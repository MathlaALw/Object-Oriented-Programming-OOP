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
