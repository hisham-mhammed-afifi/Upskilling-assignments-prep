# OOP in C#

---

## Table of Contents

1. **Core OOP Pillars in C#**
2. **Types of Object Relationships**
3. **Encapsulation & Access Modifiers in Practice**
4. **Inheritance & Polymorphism in Real Scenarios**
5. **Interfaces & Abstraction in Large Systems**
6. **Association, Aggregation, and Composition**
7. **Practical OOP Example: E-Commerce Domain**
8. **Design Patterns That Reinforce OOP**
9. **Common Pitfalls & Best Practices**

---

## 1. Core OOP Pillars in C#

### Encapsulation

- **Definition**: Bundling of data and methods that operate on that data.
- **Goal**: Hide implementation details, expose only what is necessary.

### Inheritance

- **Definition**: A class (derived/child) inherits properties and methods from another class (base/parent).
- **Goal**: Reuse existing code and reduce duplication.

### Polymorphism

- **Definition**: Objects can take on multiple forms, typically referring to method overriding or interface implementation.
- **Goal**: Provide a single interface to entities of different types.

### Abstraction

- **Definition**: Representing essential features without including background details.
- **Goal**: Create a clear separation between interface and implementation.

---

## 2. Types of Object Relationships

1. **Association**: A general “uses-a” relationship. One class uses another but there’s no strong ownership.

   - _Example_: A `Customer` class can have a method that uses a `PaymentService` class to process payments.

2. **Aggregation**: A form of association with a “has-a” relationship, but the lifespan of the contained object is not strictly bound to the container’s lifespan.

   - _Example_: A `Car` **aggregates** `Tire` objects. Tires can exist independently of the car.

3. **Composition**: A strong “owns-a” relationship where the contained object cannot exist without the container.

   - _Example_: A `House` composed of `Room` objects. Once the house is gone, the rooms have no standalone meaning.

4. **Inheritance**: An “is-a” relationship.
   - _Example_: A `Dog` is an `Animal`.

---

## 3. Encapsulation & Access Modifiers in Practice

Encapsulation is often exemplified by using private fields and exposing them via public properties:

```csharp
public class BankAccount
{
    private decimal _balance;

    // Property with validation logic
    public decimal Balance
    {
        get { return _balance; }
        private set
        {
            if (value < 0)
                throw new ArgumentException("Balance cannot be negative.");
            _balance = value;
        }
    }

    public BankAccount(decimal initialBalance)
    {
        Balance = initialBalance; // uses the property’s logic
    }

    public void Deposit(decimal amount)
    {
        if (amount <= 0)
            throw new ArgumentException("Deposit amount must be positive.");
        Balance += amount; // triggers property set logic
    }

    public void Withdraw(decimal amount)
    {
        if (amount <= 0)
            throw new ArgumentException("Withdrawal amount must be positive.");
        Balance -= amount; // triggers property set logic
    }
}
```

### Practical Tip

- Keep fields private and expose them through properties. This ensures that any business rules or validations can be enforced through the property setter.
- Use `internal` or `protected` where possible to limit scope and maintain stronger encapsulation.

---

## 4. Inheritance & Polymorphism in Real Scenarios

### Inheritance Example

Imagine a user management system:

```csharp
public class User
{
    public string Username { get; set; }
    public string Email { get; set; }

    public virtual void Login()
    {
        Console.WriteLine($"{Username} logged in with email {Email}");
    }
}

public class AdminUser : User
{
    public override void Login()
    {
        Console.WriteLine($"Admin {Username} logged in with admin privileges");
    }

    public void AccessAdminPanel()
    {
        Console.WriteLine("Accessing admin panel...");
    }
}
```

- `AdminUser` **is-a** `User` but with additional behaviors (`AccessAdminPanel`) and possibly overriding the `Login` method to reflect admin capabilities.

### Polymorphism Example

Suppose we have a `Notification` system:

```csharp
public abstract class Notification
{
    public abstract void Send(string message);
}

public class EmailNotification : Notification
{
    public override void Send(string message)
    {
        Console.WriteLine($"Email sent: {message}");
    }
}

public class SmsNotification : Notification
{
    public override void Send(string message)
    {
        Console.WriteLine($"SMS sent: {message}");
    }
}

public class PushNotification : Notification
{
    public override void Send(string message)
    {
        Console.WriteLine($"Push notification sent: {message}");
    }
}
```

- By treating `Notification` as the abstraction, the calling code can decide at runtime which concrete type to instantiate, yet the interface (i.e., `Send`) remains the same.

---

## 5. Interfaces & Abstraction in Large Systems

### Interface Example

Interfaces offer a contract without dictating implementation details. For instance, in a payment processing system:

```csharp
public interface IPaymentProcessor
{
    void ProcessPayment(decimal amount);
}

public class PayPalPaymentProcessor : IPaymentProcessor
{
    public void ProcessPayment(decimal amount)
    {
        Console.WriteLine($"Processing ${amount} through PayPal.");
    }
}

public class StripePaymentProcessor : IPaymentProcessor
{
    public void ProcessPayment(decimal amount)
    {
        Console.WriteLine($"Processing ${amount} through Stripe.");
    }
}

// Usage
public class ShoppingCart
{
    private readonly IPaymentProcessor _paymentProcessor;

    public ShoppingCart(IPaymentProcessor paymentProcessor)
    {
        _paymentProcessor = paymentProcessor;
    }

    public void Checkout(decimal amount)
    {
        _paymentProcessor.ProcessPayment(amount);
        Console.WriteLine("Checkout completed!");
    }
}
```

- Your system can easily swap out the payment processor implementation without affecting any other classes, thanks to the interface.

### Abstraction in Large Systems

- **Tip**: Use abstract classes when you have a base class that includes both shared logic and abstract methods. Use interfaces if you strictly need a contract.

---

## 6. Association, Aggregation, and Composition

### Association Example

```csharp
public class ChatService
{
    // Association: uses a Logger, but is not necessarily responsible for its creation or disposal
    public void SendMessage(string message, ILogger logger)
    {
        logger.Log($"Sending message: {message}");
        // send the message
    }
}
```

### Aggregation Example

```csharp
public class Company
{
    // Aggregation: The Company has Employees, but the Employee can exist independently (e.g., as a contractor).
    public List<Employee> Employees { get; set; } = new List<Employee>();
}

public class Employee
{
    public string Name { get; set; }
    // ...
}
```

- The `Employee` objects can survive even if `Company` ceases to exist—maybe they move to a different company.

### Composition Example

```csharp
public class Order
{
    // Composition: The Order has OrderItems that do not make sense without the Order.
    private List<OrderItem> _items = new List<OrderItem>();

    public void AddItem(int productId, int quantity, decimal price)
    {
        var item = new OrderItem(productId, quantity, price);
        _items.Add(item);
    }

    public IReadOnlyList<OrderItem> Items => _items.AsReadOnly();
}

public class OrderItem
{
    public int ProductId { get; }
    public int Quantity { get; }
    public decimal Price { get; }

    // Can't create an OrderItem without specifying details
    public OrderItem(int productId, int quantity, decimal price)
    {
        ProductId = productId;
        Quantity = quantity;
        Price = price;
    }
}
```

- An `OrderItem` is meaningful only in the context of an `Order`.

---

## 7. Practical OOP Example: E-Commerce Domain

Let’s build a mini e-commerce domain to illustrate how these relationships and principles come together.

### Step 1: Define Models

```csharp
public class Product
{
    public int Id { get; private set; }
    public string Name { get; private set; }
    public decimal Price { get; private set; }

    public Product(int id, string name, decimal price)
    {
        Id = id;
        Name = name;
        Price = price;
    }
}
```

### Step 2: A Composed `Cart` and `CartItems`

```csharp
public class CartItem
{
    public Product Product { get; }
    public int Quantity { get; private set; }

    public CartItem(Product product, int quantity)
    {
        Product = product;
        Quantity = quantity;
    }

    public void IncreaseQuantity(int quantity)
    {
        Quantity += quantity;
    }
}

public class Cart
{
    private List<CartItem> _items = new List<CartItem>();

    public void AddItem(Product product, int quantity)
    {
        var existingItem = _items.FirstOrDefault(i => i.Product.Id == product.Id);
        if (existingItem == null)
        {
            _items.Add(new CartItem(product, quantity));
        }
        else
        {
            existingItem.IncreaseQuantity(quantity);
        }
    }

    public decimal GetTotalPrice()
    {
        return _items.Sum(item => item.Product.Price * item.Quantity);
    }

    // Expose items as read-only
    public IReadOnlyList<CartItem> Items => _items.AsReadOnly();
}
```

- `Cart` **composes** `CartItem` because a `CartItem` is only valid in the context of a `Cart`.

### Step 3: Payment Abstraction (Interfaces)

```csharp
public interface IPaymentGateway
{
    bool ProcessPayment(decimal amount, string currency);
}

public class PayPalGateway : IPaymentGateway
{
    public bool ProcessPayment(decimal amount, string currency)
    {
        // PayPal API call
        Console.WriteLine($"PayPal: Processing {amount} {currency}...");
        return true;
    }
}

public class CreditCardGateway : IPaymentGateway
{
    public bool ProcessPayment(decimal amount, string currency)
    {
        // Credit card API call
        Console.WriteLine($"Credit Card: Processing {amount} {currency}...");
        return true;
    }
}
```

### Step 4: Checkout Service (Association with Payment Gateway)

```csharp
public class CheckoutService
{
    private readonly IPaymentGateway _paymentGateway;
    private readonly Cart _cart;

    public CheckoutService(IPaymentGateway paymentGateway, Cart cart)
    {
        _paymentGateway = paymentGateway;
        _cart = cart;
    }

    public void Checkout()
    {
        decimal totalAmount = _cart.GetTotalPrice();
        bool result = _paymentGateway.ProcessPayment(totalAmount, "USD");
        if (!result)
        {
            Console.WriteLine("Payment failed!");
            return;
        }

        Console.WriteLine("Payment successful. Order placed!");
    }
}
```

- `CheckoutService` uses a `Cart` and a `PaymentGateway`. This is an **association** (we inject these dependencies).

---

## 8. Design Patterns That Reinforce OOP

1. **Factory Method** (Encapsulation of object creation logic)
2. **Strategy** (Interchangeable algorithms; often used with interfaces)
3. **Singleton** (Careful—commonly overused, but can be useful for global objects like a logging context)
4. **Repository** (Abstraction over data access, keeping domain logic clean)

Example of the **Strategy** pattern in a discount scenario:

```csharp
public interface IDiscountStrategy
{
    decimal ApplyDiscount(decimal amount);
}

public class NoDiscountStrategy : IDiscountStrategy
{
    public decimal ApplyDiscount(decimal amount) => amount;
}

public class PercentageDiscountStrategy : IDiscountStrategy
{
    private readonly decimal _percentage;
    public PercentageDiscountStrategy(decimal percentage)
    {
        _percentage = percentage;
    }

    public decimal ApplyDiscount(decimal amount) => amount - (amount * _percentage);
}

public class CartService
{
    private readonly Cart _cart;
    private IDiscountStrategy _discountStrategy;

    public CartService(Cart cart, IDiscountStrategy discountStrategy)
    {
        _cart = cart;
        _discountStrategy = discountStrategy;
    }

    public decimal Checkout()
    {
        decimal totalPrice = _cart.GetTotalPrice();
        return _discountStrategy.ApplyDiscount(totalPrice);
    }
}
```

- We can change `IDiscountStrategy` at runtime, providing a flexible approach to discounts.

---

## 9. Common Pitfalls & Best Practices

1. **Overusing Inheritance**

   - Overly complex inheritance hierarchies lead to rigidity. Prefer composition over inheritance when feasible.

2. **Leaky Encapsulation**

   - Avoid publicly exposing fields or properties that can be mutated outside your control. Always keep the business rules within your class.

3. **Single Responsibility Principle (SRP)**

   - Each class should handle one primary responsibility. This keeps classes small and cohesive.

4. **Open/Closed Principle (OCP)**

   - Classes should be open for extension, closed for modification. Use polymorphism and extension methods rather than rewriting existing code.

5. **Interface Segregation Principle (ISP)**

   - Don’t force classes to implement methods they don’t need. Split large interfaces into smaller, focused ones.

6. **Dependency Inversion Principle (DIP)**

   - Rely on abstractions, not concretions (e.g., your class should depend on an `ILogger`, not a specific `FileLogger`).

7. **Avoid Premature Optimization**
   - Don’t complicate your design just for potential performance gains. Keep it simple, clear, and maintainable.

---

## Conclusion

Mastering OOP in C# involves a deep understanding of:

- **Core OOP principles** (Encapsulation, Inheritance, Polymorphism, Abstraction)
- **Object relationships** (Association, Aggregation, Composition)
- **Practical application** through well-designed classes, interfaces, and real-world patterns.

Keep refining your designs with a strong emphasis on maintainability and scalability. Real-world OOP is about trade-offs—knowing when to pick inheritance versus composition, how to isolate responsibilities, and how to keep your design flexible for future changes.

With this guide in hand, you should be able to:

1. Identify which relationships are most appropriate for your domain models.
2. Design systems that are robust, testable, and easy to evolve.
3. Leverage advanced features of C# (interfaces, abstract classes, generics, etc.) for clarity and maintainability.

---
