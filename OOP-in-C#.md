## Suggested Topics for Separate Discussions

1. **Deep Dive into the Four OOP Pillars**

   - _Subtopics_:
     - Encapsulation best practices in modern C#
     - Inheritance vs. composition (practical scenarios)
     - Polymorphism pitfalls (overriding, hiding methods, the `virtual` keyword)
     - Abstraction patterns (when to choose abstract classes vs. interfaces)

2. **Advanced Relationships & Lifecycles**

   - _Subtopics_:
     - Association vs. Aggregation vs. Composition in real systems
     - Managing object lifecycles (IoC containers, DI frameworks)
     - Mapping relationships in databases (e.g., EF Core or other ORMs)

3. **Encapsulation & Data Protection Techniques**

   - _Subtopics_:
     - C# access modifiers beyond `private/public` (e.g., `protected internal`)
     - Writing robust property setters/getters with advanced validation
     - Best practices for dealing with sensitive data (security, encryption, etc.)

4. **Polymorphism and Interface Implementation**

   - _Subtopics_:
     - Dynamic vs. static polymorphism, generics usage in C#
     - Deeper interface segregation examples (splitting large interfaces)
     - Implementing multiple interfaces gracefully (avoid collisions, naming conventions)

5. **SOLID Principles in Practice**

   - _Subtopics_:
     - Single Responsibility Principle (SRP) with real-world scenarios
     - Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion
     - Identifying and fixing “code smells” that violate SOLID

6. **Design Patterns for Maintainable Code**

   - _Subtopics_:
     - Factory, Abstract Factory, Builder (object creation patterns)
     - Strategy, Observer, Decorator (behavioral and structural patterns)
     - Repository and Unit of Work in enterprise applications
     - Using patterns to decouple subsystems (e.g., Service Layer + Repository)

---

# Deep Dive into the Four OOP Pillars

## 1. Encapsulation Best Practices in Modern C\#

**Definition**  
Encapsulation is the bundling of data (fields) and the methods (or properties) that operate on them into a single unit, while restricting direct access from the outside world. The idea is to protect the internal state and behavior of an object from unintended interference.

### 1.1 Why Encapsulation Matters

- **Maintainability**: Changes to internal logic or data representation remain invisible to external code.
- **Data Integrity**: Validation logic and checks can be centralized in property setters.
- **Abstraction of Complexity**: Consumers only need to know “what it does,” not “how it does it.”

### 1.2 Common Techniques in C\#

1. **Private Fields with Public Properties**

   ```csharp
   public class BankAccount
   {
       private decimal _balance;

       public decimal Balance
       {
           get => _balance;
           private set
           {
               if (value < 0)
                   throw new ArgumentException("Balance cannot be negative.");
               _balance = value;
           }
       }

       public BankAccount(decimal initialBalance)
       {
           Balance = initialBalance;
       }

       public void Deposit(decimal amount)
       {
           if (amount <= 0)
               throw new ArgumentException("Deposit amount must be positive.");
           Balance += amount;
       }

       // ...
   }
   ```

   - **Why?**: This setup allows a single point of validation and logic enforcement, maintaining data integrity.

2. **Auto-Properties and init** (C# 9+)

   ```csharp
   public class Product
   {
       public int Id { get; init; }
       public string Name { get; init; }
       public decimal Price { get; private set; }

       public Product(int id, string name, decimal price)
       {
           Id = id;
           Name = name;
           Price = price;
       }

       public void UpdatePrice(decimal newPrice)
       {
           if (newPrice < 0)
               throw new ArgumentException("Price cannot be negative.");
           Price = newPrice;
       }
   }
   ```

   - **Why?**: `init` ensures properties are settable only during object initialization, supporting immutable or near-immutable data models.

3. **Access Modifiers**

   - **private**: Accessible only in the same class.
   - **protected**: Accessible in the same class or derived classes.
   - **internal**: Accessible within the same assembly.
   - **protected internal**: Accessible within the same assembly or derived classes in other assemblies.
   - **private protected**: Accessible by containing class or derived classes within the same assembly.

4. **Beyond the Basics**
   - Consider using `readonly` fields if the data never changes after construction.
   - For advanced scenarios (especially micro-optimizations), direct field access can be used, but only when you are sure about the trade-offs.

---

## 2. Inheritance vs. Composition (Practical Scenarios)

**Definition**

- **Inheritance**: A mechanism where a derived class “is-a” specific type of the base class.
- **Composition**: A class “has-a” relationship with other objects that collaborate to achieve functionality.

### 2.1 When to Prefer Inheritance

- **Specialization** of an existing class:
  - Example: `AdminUser : User` (an AdminUser is still a User, but with extra privileges).
- **Shared Behavior with Variation**: Overriding virtual methods to provide specialized functionality.
- **Framework Requirements**: For instance, certain UI frameworks require deriving from a base class.

### 2.2 When to Prefer Composition

- **Flexible Code**: Composition tends to reduce tight coupling. You can swap out composed objects more easily than changing an inheritance hierarchy.
- **Avoiding Deep Hierarchies**: Overly complex inheritance trees can become fragile; composition is more resilient to change.
- **Reusing Behavior**: When you want to add features from multiple sources, composition (injecting dependencies that implement required behaviors) is cleaner than multiple inheritance (which C# doesn’t support directly, anyway).

### 2.3 Example Scenarios

1. **Inheritance Example**:

   ```csharp
   public class User
   {
       public string Username { get; set; }
       public virtual void Login()
       {
           Console.WriteLine("User logged in.");
       }
   }

   public class AdminUser : User
   {
       public override void Login()
       {
           Console.WriteLine("Admin logged in with elevated privileges.");
       }
   }
   ```

   - **Fits**: AdminUser is conceptually a specialized User.

2. **Composition Example**:

   ```csharp
   public class EmailSender
   {
       public void SendEmail(string to, string subject)
       {
           // Implementation...
       }
   }

   public class NotificationService
   {
       private readonly EmailSender _emailSender;

       public NotificationService(EmailSender emailSender)
       {
           _emailSender = emailSender;
       }

       public void Notify(string message)
       {
           // Use the composed EmailSender
           _emailSender.SendEmail("admin@company.com", message);
       }
   }
   ```

   - **Fits**: `NotificationService` “has-an” `EmailSender` but does not inherit from it. Swapping `EmailSender` for an `SmsSender` is straightforward.

---

## 3. Polymorphism Pitfalls (Overriding, Hiding Methods, the `virtual` Keyword)

**Definition**  
Polymorphism allows objects of different types to be treated uniformly, usually by sharing a base type or interface.

### 3.1 Overriding vs. Hiding

1. **Overriding**

   - Uses the `override` keyword.
   - Requires the base method to be marked `virtual`, `abstract`, or `override`.
   - The base version can still be accessed by `base.MethodName()`.

   ```csharp
   public class BaseClass
   {
       public virtual void DoWork()
       {
           Console.WriteLine("Base DoWork");
       }
   }

   public class DerivedClass : BaseClass
   {
       public override void DoWork()
       {
           Console.WriteLine("Derived DoWork");
       }
   }
   ```

2. **Hiding**

   - Uses the `new` keyword (not the same as `override`).
   - Tells the compiler you are intentionally hiding the base class method.
   - Can create confusion when casting objects to a base type.

   ```csharp
   public class HidingClass : BaseClass
   {
       public new void DoWork()
       {
           Console.WriteLine("HidingClass DoWork");
       }
   }
   ```

### 3.2 Common Pitfalls

- **Accidental Hiding**: Missing `override` might inadvertently hide the base method.
- **Rigid Hierarchies**: Overusing polymorphism can lead to tight coupling, making changes more expensive.
- **Performance**: Virtual dispatch has a small overhead, but in most scenarios, it’s negligible compared to the architectural benefits.

### 3.3 Best Practices

- Mark methods as `virtual` only when you expect them to be overridden.
- Use `sealed` on overridden methods to prevent further overrides if extension beyond that point makes little sense.
- If you see `new` in your code frequently, reevaluate whether you need inheritance or a different design strategy (e.g., composition or interfaces).

---

## 4. Abstraction Patterns (When to Choose Abstract Classes vs. Interfaces)

**Definition**

- **Abstraction**: Exposing essential features of an object while hiding underlying details.
- **Interfaces**: Define a contract with no implementation (in classic C#), though modern C# versions can include default implementations.
- **Abstract Classes**: Provide partial implementation, plus members that derived classes must implement.

### 4.1 Interfaces

- **Multiple Implementations**: A class can implement multiple interfaces.
- **No State** (traditionally): Interfaces don’t hold data, though default interface methods can have some limited implementation in recent C# versions.
- **Behavioral Contracts**: Perfect when you need an interchangeable “plug-in” style approach.

```csharp
public interface IPaymentGateway
{
    bool ProcessPayment(decimal amount, string currency);
}

public class PayPalGateway : IPaymentGateway
{
    public bool ProcessPayment(decimal amount, string currency)
    {
        // Implementation...
        return true;
    }
}
```

### 4.2 Abstract Classes

- **Single Inheritance**: A class can only inherit from one base class, abstract or not.
- **Partial Implementation**: You can define shared logic in the abstract class while leaving some members abstract.
- **Use When**:
  - You have a “base” concept that multiple derived classes can share.
  - You want to ensure all derived classes have certain functionality or fields.
  - You need to maintain protected members or state across derived classes.

```csharp
public abstract class Notification
{
    protected string Recipient { get; set; }

    public Notification(string recipient)
    {
        Recipient = recipient;
    }

    public abstract void Send(string message);
}

public class SmsNotification : Notification
{
    public SmsNotification(string recipient) : base(recipient) { }

    public override void Send(string message)
    {
        Console.WriteLine($"Sending SMS to {Recipient}: {message}");
    }
}
```

### 4.3 Choosing Between Abstract Classes and Interfaces

1. **Use an Interface** if:

   - You only need to define a contract (methods, properties, events), with no shared state or code.
   - You anticipate needing to plug in multiple unrelated implementations.
   - You want to enable multiple “types of capabilities” for one class (multiple interfaces).

2. **Use an Abstract Class** if:

   - You have partial implementation or state that applies to all subclasses.
   - You want to enforce a strict inheritance hierarchy.
   - You need to shield some parts of the implementation as `protected` for derived classes.

3. **Mixing Both**
   - A class can implement multiple interfaces while also inheriting from one abstract class.
   - Real-world solutions often use a combination: a base abstract class for common logic and interfaces for pluggable capabilities.

---

# Advanced Relationships & Lifecycles

## 1. Association vs. Aggregation vs. Composition in Real Systems

### 1.1 Recap of Definitions

1. **Association:** A general “uses-a” relationship—one object references another for a particular function but does not imply strong ownership.
2. **Aggregation:** A “has-a” relationship in which the container (parent) holds a reference to the child object, but the child can outlive the parent.
3. **Composition:** A “owns-a” relationship that implies the child object’s lifecycle is tightly bound to the parent—if the parent is destroyed, the child should not exist independently.

### 1.2 Practical Scenarios

1. **Association Example: Loggers or Services**

   ```csharp
   public class ReportGenerator
   {
       public void GenerateReport(ILogger logger)
       {
           // Uses the logger but does not own it
           logger.Log("Generating report...");
       }
   }
   ```

   - **Why it’s Association**: `ReportGenerator` just uses an `ILogger` instance; it doesn’t create or destroy it. The `ILogger` can exist independently.

2. **Aggregation Example: Company and Employees**

   ```csharp
   public class Company
   {
       public List<Employee> Employees { get; set; } = new List<Employee>();
       // The Company aggregates Employees,
       // but Employees can exist without the Company (e.g., as a contractor).
   }
   ```

   - **Why it’s Aggregation**: Employees can be removed from one Company and added to another. Their existence isn’t strictly dependent on the Company object.

3. **Composition Example: Order and OrderItems**

   ```csharp
   public class Order
   {
       private List<OrderItem> _items = new List<OrderItem>();

       public void AddItem(int productId, int quantity, decimal price)
       {
           var item = new OrderItem(productId, quantity, price);
           _items.Add(item);
       }
   }

   public class OrderItem
   {
       public int ProductId { get; }
       public int Quantity { get; }
       public decimal Price { get; }

       public OrderItem(int productId, int quantity, decimal price)
       {
           ProductId = productId;
           Quantity = quantity;
           Price = price;
       }
   }
   ```

   - **Why it’s Composition**: An `OrderItem` makes no sense outside the context of its `Order`. If the `Order` is deleted, so are its `OrderItem`s.

### 1.3 Choosing the Right Relationship

- **Association**: When you need a loose connection—services, utilities, or external dependencies that are not “owned.”
- **Aggregation**: When multiple entities can live independently and the parent is more of a collection holder.
- **Composition**: When the parent truly owns the child, and you want a strong guarantee that these objects live and die together.

---

## 2. Managing Object Lifecycles (IoC Containers, DI Frameworks)

### 2.1 Why Lifecycles Matter

In modern C# applications—particularly those using ASP.NET Core or other frameworks—the way you manage an object’s lifecycle (creation, reuse, and disposal) directly affects:

- **Resource Usage**: Preventing memory leaks or unnecessary instantiation.
- **Thread Safety**: Especially important for services that maintain internal state.
- **Testability**: Being able to inject mocks or stubs during automated tests.

### 2.2 Common Lifetime Configurations

1. **Transient**: A new instance is provided every time it is requested.
2. **Scoped**: One instance per scope (often a web request in ASP.NET).
3. **Singleton**: A single instance is reused for the lifetime of the application.

In ASP.NET Core, for example:

```csharp
services.AddTransient<IEmailSender, SmtpEmailSender>();
services.AddScoped<IOrderRepository, OrderRepository>();
services.AddSingleton<ILoggingService, LoggingService>();
```

### 2.3 IoC Containers & DI Frameworks

1. **Built-in .NET DI**: ASP.NET Core provides a lightweight IoC container by default.
2. **Third-Party Containers**: Autofac, Ninject, StructureMap, etc. offer more advanced features:
   - Automatic discovery of types (Assembly scanning)
   - Interception and decorators
   - Complex lifetime scopes (e.g., child containers)

### 2.4 Handling Relationships with DI

- **Loose Coupling with Interfaces**: Classes depend on abstractions (`IService`) rather than concrete implementations (`Service`).
- **Injecting Dependent Objects**: For association or aggregation, inject dependencies via the constructor.
- **Composition**: Typically represented by directly creating child objects within the parent, but if you require external services for the children, you might still use DI to create them.

```csharp
public class ShoppingCart
{
    private readonly List<CartItem> _items = new();
    private readonly IDiscountStrategy _discountStrategy;

    // Aggregation: _discountStrategy can outlive ShoppingCart
    public ShoppingCart(IDiscountStrategy discountStrategy)
    {
        _discountStrategy = discountStrategy;
    }

    public void AddItem(Product product, int quantity)
    {
        _items.Add(new CartItem(product, quantity));
    }
}
```

---

## 3. Mapping Relationships in Databases (EF Core & Other ORMs)

### 3.1 EF Core Relationship Types

1. **One-to-Many**: A `Company` has many `Employees`.
2. **One-to-One**: A `User` might have a single `UserProfile`.
3. **Many-to-Many**: A `Student` can enroll in many `Courses`, and a `Course` can have many `Students`.
4. **Owned Entities**: Typically represent composition. The owned entity’s data is contained in the same table as the owner in EF Core.

#### Example: One-to-Many

```csharp
public class Company
{
    public int Id { get; set; }
    public string Name { get; set; }
    public List<Employee> Employees { get; set; } = new();
}

public class Employee
{
    public int Id { get; set; }
    public string FullName { get; set; }
    public int CompanyId { get; set; }
    public Company Company { get; set; }  // Navigation property
}
```

**EF Core Config**:

```csharp
modelBuilder.Entity<Company>()
    .HasMany(c => c.Employees)
    .WithOne(e => e.Company)
    .HasForeignKey(e => e.CompanyId);
```

- This is an **aggregation** in code terms (the `Company` is not strictly “owning” the existence of `Employee`).

#### Example: Owned Entity (Composition)

```csharp
public class Order
{
    public int Id { get; set; }
    public List<OrderItem> Items { get; set; } = new();
}

[Owned]
public class OrderItem
{
    public int ProductId { get; set; }
    public int Quantity { get; set; }
    public decimal Price { get; set; }
}
```

**EF Core Config**:

```csharp
modelBuilder.Entity<Order>()
    .OwnsMany(o => o.Items);
```

- **Composition**: `OrderItem` is owned by the `Order`; EF Core will likely store them in a separate table with a foreign key referencing the `Order`.

### 3.2 Considerations for Aggregation vs. Composition in Databases

- **Aggregation**: Usually implies separate tables with foreign keys and the possibility of reassigning or using the child in other parent objects (e.g., an `Employee` moving to a new `Company`).
- **Composition**: Often modeled as an “owned entity” or embedded document (in NoSQL). The child typically cannot exist independently.

### 3.3 Practical Pitfalls and Tips

- **Cascade Deletes**: In composition scenarios, ensure cascade delete is configured so child records are removed automatically.
- **Lazy Loading vs. Eager Loading**: For associated or aggregated entities, decide if you want to load them on-demand or all at once.
- **Performance**: Many relationships can lead to complex joins. Consider the trade-off between normalization and performance.

---

# Encapsulation & Data Protection Techniques

## 1. C# Access Modifiers Beyond `private` and `public`

### 1.1 Overview of Additional Modifiers

1. **`protected`**

   - Accessible within the defining class and any derived classes.
   - Often used to allow subclass-specific overrides or extensions.

2. **`internal`**

   - Accessible within the same assembly (project).
   - Useful for code that doesn’t need public exposure but must be visible to other types in the same assembly.

3. **`protected internal`**

   - Accessible within the same assembly (`internal`) or within derived classes in other assemblies (`protected`).
   - Rarely used in everyday scenarios, but can be beneficial for libraries offering partial extension points.

4. **`private protected` (C# 7.2+)**
   - Accessible only within the declaring class or derived classes _within the same assembly_.
   - Offers finer-grained control if you want to limit scope to derived classes without exposing details to the entire assembly.

### 1.2 Example Use Cases

```csharp
public class BaseController
{
    // protected internal: accessible by derived classes (even if they’re in other assemblies),
    // and also accessible to other classes in the same assembly.
    protected internal string RoutePrefix { get; set; }

    // private protected: only accessible by derived classes in the same assembly.
    private protected string ConnectionString { get; set; }

    public void BaseAction()
    {
        Console.WriteLine("Base action executed.");
    }
}

internal class DerivedController : BaseController
{
    public void PerformAction()
    {
        // RoutePrefix is accessible (protected internal).
        // ConnectionString is accessible since both classes share the same assembly (private protected).
    }
}
```

- Using **`protected internal`** might be useful in a framework library if you want to give external consumers the ability to derive and extend classes but only in a controlled way.
- **`private protected`** narrows this further to your in-assembly derived classes.

### 1.3 Choosing the Right Modifier

- **Security**: Don’t expose fields or members unnecessarily—least privilege principle applies.
- **API Design**: If you’re building a class library for external use, carefully consider which parts of your API to open for extension to avoid breaking changes later.

---

## 2. Writing Robust Property Setters/Getters with Advanced Validation

### 2.1 Why Validation in Properties Is Crucial

- **Data Integrity**: Ensuring invalid data never gets assigned in the first place.
- **Single Responsibility**: Containing logic in property setters keeps validation localized and consistent.

### 2.2 Examples of Advanced Validation

```csharp
public class Employee
{
    private string _fullName;

    public string FullName
    {
        get => _fullName;
        set
        {
            // Basic validation example
            if (string.IsNullOrWhiteSpace(value))
                throw new ArgumentException("Full name cannot be empty or whitespace.");

            // Possibly advanced checks, like length limits or banned characters
            if (value.Length > 100)
                throw new ArgumentException("Full name cannot exceed 100 characters.");

            _fullName = value;
        }
    }

    private decimal _salary;

    public decimal Salary
    {
        get => _salary;
        set
        {
            // Salary-specific validation
            if (value < 0)
                throw new ArgumentOutOfRangeException(nameof(value), "Salary cannot be negative.");
            _salary = value;
        }
    }
}
```

### 2.3 Additional Strategies

- **Throwing Custom Exceptions**: Instead of `ArgumentException`, create domain-specific exceptions (e.g., `InvalidSalaryException`) to convey meaning.
- **Property-Changed Notifications**: In WPF or Blazor, you may leverage `INotifyPropertyChanged` for real-time UI updates.
- **Fluent Validation**: In more complex scenarios (especially with multiple related properties), consider a separate validation library (e.g., FluentValidation) for systematic rule definitions.

---

## 3. Best Practices for Dealing with Sensitive Data (Security, Encryption, etc.)

### 3.1 Identifying Sensitive Data

1. **Personal Identifiable Information (PII)**: Names, emails, phone numbers, addresses.
2. **Financial/Payment Data**: Credit card numbers, bank details, payment tokens.
3. **Authentication Secrets**: Passwords, API keys, tokens.

### 3.2 Storing Secrets Securely

1. **Use Secure Storage**:

   - **Azure Key Vault**, **AWS Secrets Manager**, or local **user-secrets** in .NET for development.
   - Avoid hardcoding secrets or storing them in source control.

2. **Encryption at Rest**:

   - If storing sensitive data in a database, consider column-level encryption or entire-database encryption (e.g., Transparent Data Encryption in SQL Server).
   - For files, use either .NET’s **Data Protection APIs** or a third-party library for encryption/decryption.

3. **Encryption in Transit**:
   - Always use **HTTPS** or **TLS** for communication between services.
   - In microservice architectures, mutual TLS can secure service-to-service traffic.

### 3.3 Implementing Secure Properties

1. **Hashed or Salted Passwords**: Never store passwords in plain text.
2. **Secure Strings** (on older .NET platforms): Use `System.Security.SecureString` where appropriate, though be aware this is less emphasized in .NET 5+ and 6+ due to limited benefits on modern OS.
3. **Auditing and Logging**: Redact sensitive fields (like credit card info) from logs.

```csharp
public class UserCredentials
{
    private string _hashedPassword;

    public string Password
    {
        // Typically, do not store or expose the raw password
        set
        {
            // Hash + salt the password and store that
            _hashedPassword = HashingService.Hash(value);
        }
    }

    public bool ValidatePassword(string input)
    {
        // Compare hashed input with stored hashed password
        return HashingService.Verify(input, _hashedPassword);
    }
}
```

### 3.4 Compliance Considerations

- **GDPR** (Europe), **CCPA** (California), and other data protection regulations require careful handling and potential anonymization or pseudonymization of data.
- **Auditing**: Keep track of data access or modifications for compliance reporting.

---

# Polymorphism and Interface Implementation

## 1. Dynamic vs. Static Polymorphism, Generics Usage in C#

### 1.1 Dynamic (Runtime) Polymorphism

**Key Concepts**

- Achieved through **inheritance** and **virtual methods**, **abstract methods**, or **interfaces**.
- Allows objects of different types to be treated uniformly at **runtime**.
- C# dispatches method calls based on the actual object type (rather than the declared reference type).

**Examples**

1. **Virtual/Override**:

   ```csharp
   public class Animal
   {
       public virtual void Speak()
       {
           Console.WriteLine("Some generic animal sound");
       }
   }

   public class Dog : Animal
   {
       public override void Speak()
       {
           Console.WriteLine("Woof!");
       }
   }

   // Using dynamic polymorphism
   Animal myDog = new Dog();
   myDog.Speak(); // Outputs "Woof!"
   ```

2. **Interface-based**:

   ```csharp
   public interface INotifier
   {
       void Notify(string message);
   }

   public class EmailNotifier : INotifier
   {
       public void Notify(string message)
       {
           Console.WriteLine($"Email: {message}");
       }
   }

   public class SmsNotifier : INotifier
   {
       public void Notify(string message)
       {
           Console.WriteLine($"SMS: {message}");
       }
   }

   // Polymorphic usage
   INotifier notifier = new EmailNotifier();
   notifier.Notify("Hello!");
   ```

### 1.2 Static (Compile-Time) Polymorphism

**Key Concepts**

- Achieved through **method overloading** and **generics**.
- The compiler determines which method to call based on parameter lists, types, and generic constraints at **compile time**.

**Examples**

1. **Method Overloading**:

   ```csharp
   public class MathOperations
   {
       public int Add(int x, int y) => x + y;
       public double Add(double x, double y) => x + y;
   }

   // Overloaded methods; the correct Add method is chosen by the compiler based on argument types.
   ```

2. **Generics**:

   ```csharp
   public class DataStorage<T>
   {
       private T _value;

       public void Store(T value) => _value = value;
       public T Retrieve() => _value;
   }

   // The type parameter T is resolved at compile time
   DataStorage<int> intStorage = new DataStorage<int>();
   intStorage.Store(42);
   int storedValue = intStorage.Retrieve();
   ```

**Generics Best Practices**

- Use generics to create **type-safe** collections and methods that reduce code duplication.
- Apply **constraints** (e.g., `where T : class`, `where T : new()`) to limit or specify acceptable generic types.

---

## 2. Deeper Interface Segregation Examples (Splitting Large Interfaces)

### 2.1 Interface Segregation Principle (ISP)

**Definition**

- Part of SOLID principles: “No client should be forced to depend on methods it does not use.”
- Essentially, **keep interfaces small** and focused on one specific area of functionality.

### 2.2 Common Problems with Large Interfaces

1. **God Interfaces**: An interface that has too many methods, forcing classes to implement behaviors they don’t need or throwing `NotImplementedException`.
2. **Tight Coupling**: Changes to the large interface ripple through many unrelated classes.

### 2.3 Splitting Large Interfaces

**Before** (Large Interface):

```csharp
public interface IOrderProcessor
{
    void ProcessOrder(Order order);
    bool ValidatePaymentInfo(PaymentInfo payment);
    void ApplyDiscount(Order order, decimal discount);
    void SendConfirmationEmail(Order order);
    void GenerateInvoice(Order order);
}
```

- Any class implementing `IOrderProcessor` must define all five methods—even if some are irrelevant.

**After** (Separated Interfaces):

```csharp
public interface IOrderProcessor
{
    void ProcessOrder(Order order);
}

public interface IPaymentValidator
{
    bool ValidatePaymentInfo(PaymentInfo payment);
}

public interface IDiscountService
{
    void ApplyDiscount(Order order, decimal discount);
}

public interface INotificationService
{
    void SendConfirmationEmail(Order order);
}

public interface IInvoiceGenerator
{
    void GenerateInvoice(Order order);
}
```

- Classes can implement only the interfaces relevant to them, adhering to ISP.

---

## 3. Implementing Multiple Interfaces Gracefully

### 3.1 Avoiding Member Name Collisions

When implementing multiple interfaces that contain methods with the same signature (e.g., `void Start()`), you can face naming collisions. C# provides **explicit interface implementation** to handle this.

**Example**

```csharp
public interface IEngine
{
    void Start();
}

public interface IHeater
{
    void Start();
}

public class HybridCar : IEngine, IHeater
{
    // Explicit interface implementations
    void IEngine.Start()
    {
        Console.WriteLine("Engine started.");
    }

    void IHeater.Start()
    {
        Console.WriteLine("Heater started.");
    }

    // If you call Start() from an instance of HybridCar,
    // the compiler won't know which interface method to call
    // unless you cast to the specific interface:
    // ((IEngine)myCar).Start();
    // ((IHeater)myCar).Start();
}
```

- This approach **resolves collision** but can reduce discoverability of members if you don’t want them exposed on the class type directly.
- Alternatively, rename methods or restructure interfaces to avoid overlap if possible.

### 3.2 Naming Conventions

- **Prefixing**: Some developers prefix interface methods (e.g., `IEngine.EngineStart()`, `IHeater.HeaterStart()`) to avoid collisions, but this can clutter method names.
- **Refactoring**: If collisions occur frequently, refactor interfaces or keep them small and specialized to reduce the likelihood of overlapping method names.

### 3.3 Combining Small Interfaces

A class can implement multiple small interfaces if it naturally provides all those capabilities.

```csharp
public class OrderService : IOrderProcessor, IPaymentValidator
{
    public void ProcessOrder(Order order)
    {
        // Implementation
    }

    public bool ValidatePaymentInfo(PaymentInfo payment)
    {
        // Implementation
        return true;
    }
}
```

- The consumer code can treat `OrderService` as either `IOrderProcessor` or `IPaymentValidator` as needed, improving testability and flexibility.

---

# SOLID Principles in Practice

## 1. Single Responsibility Principle (SRP) with Real-World Scenarios

### 1.1 SRP Defined

- **Principle**: “A class should have one, and only one, reason to change.”
- **Goal**: Keep each class focused on a single area of responsibility.

### 1.2 Real-World Scenario: Order Processing

**Non-SRP Example**

```csharp
public class OrderService
{
    public void PlaceOrder(Order order)
    {
        // 1. Validate order details
        if (order.Items.Count == 0)
            throw new Exception("No items in the order.");

        // 2. Process payment
        ProcessPayment(order);

        // 3. Send confirmation email
        SendConfirmationEmail(order);

        // 4. Generate invoice
        GenerateInvoice(order);
    }

    private void ProcessPayment(Order order) { /* Payment logic */ }
    private void SendConfirmationEmail(Order order) { /* Email logic */ }
    private void GenerateInvoice(Order order) { /* Invoice logic */ }
}
```

- **Problems**:
  - **Too many reasons to change**: Payment logic changes, email template updates, or invoice format modifications would all force this class to be edited.
  - Harder to test— you must mock or stub multiple unrelated dependencies.

**SRP-Compliant Example**

```csharp
public class OrderValidator
{
    public void Validate(Order order)
    {
        if (order.Items.Count == 0)
            throw new Exception("No items in the order.");
    }
}

public class PaymentProcessor
{
    public void ProcessPayment(Order order)
    {
        // Payment logic
    }
}

public class EmailNotifier
{
    public void SendConfirmationEmail(Order order)
    {
        // Email logic
    }
}

public class InvoiceGenerator
{
    public void GenerateInvoice(Order order)
    {
        // Invoice logic
    }
}

public class OrderService
{
    private readonly OrderValidator _validator;
    private readonly PaymentProcessor _paymentProcessor;
    private readonly EmailNotifier _emailNotifier;
    private readonly InvoiceGenerator _invoiceGenerator;

    public OrderService(OrderValidator validator,
                        PaymentProcessor paymentProcessor,
                        EmailNotifier emailNotifier,
                        InvoiceGenerator invoiceGenerator)
    {
        _validator = validator;
        _paymentProcessor = paymentProcessor;
        _emailNotifier = emailNotifier;
        _invoiceGenerator = invoiceGenerator;
    }

    public void PlaceOrder(Order order)
    {
        _validator.Validate(order);
        _paymentProcessor.ProcessPayment(order);
        _emailNotifier.SendConfirmationEmail(order);
        _invoiceGenerator.GenerateInvoice(order);
    }
}
```

- **Benefits**:
  - Each class has a single responsibility, making the code more modular and testable.
  - Easy to modify and extend individual pieces without breaking the entire order flow.

---

## 2. The Other Four SOLID Principles

### 2.1 Open/Closed Principle (OCP)

- **Principle**: “Software entities should be open for extension, but closed for modification.”
- **Goal**: Add new features by extending existing code rather than modifying it directly.

**Example**:  
Suppose you have a shipping cost calculator that supports multiple shipping providers (DHL, FedEx, etc.).

**Without OCP**

```csharp
public class ShippingCalculator
{
    public decimal CalculateCost(Order order, string provider)
    {
        if (provider == "DHL")
        {
            // DHL pricing logic
        }
        else if (provider == "FedEx")
        {
            // FedEx pricing logic
        }
        // ... another provider, another if-else
        return 0;
    }
}
```

- **Issues**: Every time you add a new shipping provider, you must modify (and thus risk breaking) this method.

**With OCP in Mind**

```csharp
public interface IShippingProvider
{
    decimal CalculateCost(Order order);
}

public class DHLProvider : IShippingProvider
{
    public decimal CalculateCost(Order order)
    {
        // DHL pricing logic
        return 10; // example
    }
}

public class FedExProvider : IShippingProvider
{
    public decimal CalculateCost(Order order)
    {
        // FedEx pricing logic
        return 12; // example
    }
}

public class ShippingCalculator
{
    public decimal CalculateCost(Order order, IShippingProvider provider)
    {
        return provider.CalculateCost(order);
    }
}
```

- **Benefits**: To add a new provider, you create a new class implementing `IShippingProvider`; you don’t change the existing classes.

### 2.2 Liskov Substitution Principle (LSP)

- **Principle**: “Subtypes must be substitutable for their base types.”
- **Goal**: Derived classes should behave the same way as the base class from the client’s perspective, without surprising side effects.

**Violating LSP**

```csharp
public class Rectangle
{
    public virtual int Width { get; set; }
    public virtual int Height { get; set; }
}

public class Square : Rectangle
{
    public override int Width
    {
        set { base.Width = base.Height = value; }
    }

    public override int Height
    {
        set { base.Width = base.Height = value; }
    }
}
```

- **Problem**: A `Square` forcibly sets both width and height, so using a `Square` in place of a `Rectangle` can cause unexpected behavior in algorithms expecting `Width` and `Height` to be independently settable.

**Fix**

- Separate the concepts or ensure the interface/contract is flexible enough to handle `Square` differently. Alternatively, avoid inheritance for shapes with different constraints.

### 2.3 Interface Segregation Principle (ISP)

- **Principle**: “No client should be forced to depend on methods it does not use.”
- **Goal**: Keep interfaces small and focused, splitting large “god” interfaces into specific ones.

**Example**

```csharp
public interface IDevice
{
    void Print(string text);
    void Scan();
    void Fax();
}
```

- **Issue**: A basic printer that can’t fax or scan is forced to implement unused methods.

**Refined**

```csharp
public interface IPrinter
{
    void Print(string text);
}

public interface IScanner
{
    void Scan();
}

public interface IFax
{
    void Fax();
}
```

- Classes implement only the interfaces they need.

### 2.4 Dependency Inversion Principle (DIP)

- **Principle**: “Depend on abstractions, not on concretions.”
- **Goal**: High-level modules shouldn’t depend on low-level modules. Both should depend on abstractions (interfaces, abstract classes).

**Example**

```csharp
// Without DIP
public class ReportService
{
    private PdfReportGenerator _generator = new PdfReportGenerator();

    public void GenerateReport()
    {
        _generator.GeneratePdf();
    }
}
```

- **Issue**: `ReportService` is tightly coupled to `PdfReportGenerator`. Changing the report format means editing `ReportService`.

**With DIP**

```csharp
public interface IReportGenerator
{
    void GenerateReport();
}

public class PdfReportGenerator : IReportGenerator
{
    public void GenerateReport()
    {
        // PDF logic
    }
}

public class HtmlReportGenerator : IReportGenerator
{
    public void GenerateReport()
    {
        // HTML logic
    }
}

public class ReportService
{
    private readonly IReportGenerator _generator;

    public ReportService(IReportGenerator generator)
    {
        _generator = generator;
    }

    public void GenerateReport()
    {
        _generator.GenerateReport();
    }
}
```

- **Benefit**: `ReportService` now depends on `IReportGenerator`. Switching from PDF to HTML reporting requires no changes to `ReportService`.

---

## 3. Identifying and Fixing “Code Smells” That Violate SOLID

### 3.1 “Code Smell” Indicators

1. **Long Method or God Class**
   - Likely violates SRP: too many reasons to change.
   - **Fix**: Extract smaller classes or services with focused responsibilities.
2. **Rigid Switch/If-Else Chains**
   - Violates OCP: you keep adding conditions to handle new cases.
   - **Fix**: Use polymorphism or design patterns like **Strategy** or **Factory Method**.
3. **Excessive Overrides**
   - Potential LSP violation: If overriding leads to unexpected behavior for base-class clients.
   - **Fix**: Rethink class hierarchy, consider separate types or use composition.
4. **Fat Interfaces**
   - Violates ISP: Classes implement methods they don’t need.
   - **Fix**: Split into smaller, more cohesive interfaces.
5. **Tight Coupling to Concrete Classes**
   - Violates DIP: Hard-coded dependencies are scattered throughout the code.
   - **Fix**: Introduce interfaces/abstractions and leverage dependency injection frameworks.

### 3.2 Example: Refactoring a God Class

**Before**

```csharp
public class CustomerManager
{
    public void RegisterCustomer(Customer customer)
    {
        // 1. Validate
        // 2. Save to database
        // 3. Send welcome email
        // 4. Update CRM system
    }
}
```

- **Smells**:
  - **SRP**: One class does multiple tasks (validation, persistence, emailing, CRM integration).
  - Potential **DIP** violation if it directly depends on a concrete CRM library or SMTP client.

**After**

```csharp
public class CustomerValidator
{
    public void Validate(Customer customer) { /* ... */ }
}

public class CustomerRepository
{
    public void Save(Customer customer) { /* ... */ }
}

public interface INotificationService
{
    void SendWelcomeEmail(Customer customer);
}

public class EmailNotificationService : INotificationService
{
    public void SendWelcomeEmail(Customer customer) { /* ... */ }
}

public class CrmService
{
    public void UpdateCrm(Customer customer) { /* ... */ }
}

public class CustomerManager
{
    private readonly CustomerValidator _validator;
    private readonly CustomerRepository _repository;
    private readonly INotificationService _notificationService;
    private readonly CrmService _crmService;

    public CustomerManager(
        CustomerValidator validator,
        CustomerRepository repository,
        INotificationService notificationService,
        CrmService crmService)
    {
        _validator = validator;
        _repository = repository;
        _notificationService = notificationService;
        _crmService = crmService;
    }

    public void RegisterCustomer(Customer customer)
    {
        _validator.Validate(customer);
        _repository.Save(customer);
        _notificationService.SendWelcomeEmail(customer);
        _crmService.UpdateCrm(customer);
    }
}
```

- **Improvements**:
  - Each class has a distinct responsibility—**SRP** is restored.
  - `CustomerManager` depends on abstractions (e.g., `INotificationService`) for sending emails—**DIP** compliance.

---

# Design Patterns for Maintainable Code

## 1. Object Creation Patterns

### 1.1 Factory Method

**Intent**

- Define an interface for creating an object, but let subclasses decide which class to instantiate.

**Scenario**

- You have a base class that needs to create objects, but you want to delegate the choice of object type to derived classes.

**Example**

```csharp
public abstract class Document
{
    public abstract void Print();
}

public class PdfDocument : Document
{
    public override void Print() => Console.WriteLine("Printing PDF document...");
}

public class WordDocument : Document
{
    public override void Print() => Console.WriteLine("Printing Word document...");
}

// Factory Method
public abstract class DocumentCreator
{
    public abstract Document CreateDocument();
}

public class PdfCreator : DocumentCreator
{
    public override Document CreateDocument() => new PdfDocument();
}

public class WordCreator : DocumentCreator
{
    public override Document CreateDocument() => new WordDocument();
}

// Usage
DocumentCreator creator = new PdfCreator();
Document doc = creator.CreateDocument();
doc.Print();
```

- **Key Benefit**: You isolate the object creation logic in one place and can introduce new document types without modifying existing code.

### 1.2 Abstract Factory

**Intent**

- Provide an interface for creating families of related objects without specifying their concrete classes.

**Scenario**

- You want to create multiple related objects (e.g., GUI elements—buttons, text fields) that vary across different “themes” or “platforms.”

**Example**

```csharp
// Abstract Product A
public interface IButton
{
    void Render();
}

// Abstract Product B
public interface ITextBox
{
    void Render();
}

// Concrete Products
public class WinButton : IButton
{
    public void Render() => Console.WriteLine("Rendering Windows button...");
}

public class WinTextBox : ITextBox
{
    public void Render() => Console.WriteLine("Rendering Windows text box...");
}

public class MacButton : IButton
{
    public void Render() => Console.WriteLine("Rendering Mac button...");
}

public class MacTextBox : ITextBox
{
    public void Render() => Console.WriteLine("Rendering Mac text box...");
}

// Abstract Factory
public interface IUIFactory
{
    IButton CreateButton();
    ITextBox CreateTextBox();
}

// Concrete Factories
public class WinFactory : IUIFactory
{
    public IButton CreateButton() => new WinButton();
    public ITextBox CreateTextBox() => new WinTextBox();
}

public class MacFactory : IUIFactory
{
    public IButton CreateButton() => new MacButton();
    public ITextBox CreateTextBox() => new MacTextBox();
}

// Usage
IUIFactory factory = new MacFactory();
IButton button = factory.CreateButton();
ITextBox textBox = factory.CreateTextBox();
button.Render();
textBox.Render();
```

- **Key Benefit**: Ensures consistent object families (all “Mac” widgets together, or all “Windows” widgets together) while letting you easily swap entire sets of products.

### 1.3 Builder

**Intent**

- Separate the construction of a complex object from its representation, so that the same construction process can create different representations.

**Scenario**

- You need to build objects that require multiple steps (e.g., assembling parts of a car or creating a complex configuration object).

**Example**

```csharp
public class Car
{
    public string Engine { get; set; }
    public string Wheels { get; set; }
    public string PaintColor { get; set; }
}

public interface ICarBuilder
{
    void BuildEngine();
    void BuildWheels();
    void Paint(string color);
    Car GetResult();
}

public class SportsCarBuilder : ICarBuilder
{
    private Car _car = new Car();

    public void BuildEngine() => _car.Engine = "V8 Engine";
    public void BuildWheels() => _car.Wheels = "Sport Wheels";
    public void Paint(string color) => _car.PaintColor = color;
    public Car GetResult() => _car;
}

public class CarDirector
{
    public void ConstructRedSportsCar(ICarBuilder builder)
    {
        builder.BuildEngine();
        builder.BuildWheels();
        builder.Paint("Red");
    }
}

// Usage
ICarBuilder builder = new SportsCarBuilder();
CarDirector director = new CarDirector();
director.ConstructRedSportsCar(builder);
Car car = builder.GetResult();
Console.WriteLine($"Car has {car.Engine}, {car.Wheels}, painted {car.PaintColor}.");
```

- **Key Benefit**: You can reuse the same construction process with different builders to create various object variants.

---

## 2. Behavioral and Structural Patterns

### 2.1 Strategy

**Intent**

- Define a family of algorithms, encapsulate each one, and make them interchangeable. Let the algorithm vary independently from clients.

**Scenario**

- You have multiple ways to perform a specific operation (e.g., different sorting algorithms, discount strategies, or payment methods).

**Example**

```csharp
public interface IDiscountStrategy
{
    decimal ApplyDiscount(decimal total);
}

public class NoDiscount : IDiscountStrategy
{
    public decimal ApplyDiscount(decimal total) => total;
}

public class SeasonalDiscount : IDiscountStrategy
{
    public decimal ApplyDiscount(decimal total) => total * 0.9m; // 10% off
}

public class OrderService
{
    private readonly IDiscountStrategy _discountStrategy;

    public OrderService(IDiscountStrategy discountStrategy)
    {
        _discountStrategy = discountStrategy;
    }

    public decimal CalculateFinalPrice(decimal total)
    {
        return _discountStrategy.ApplyDiscount(total);
    }
}

// Usage
var service = new OrderService(new SeasonalDiscount());
Console.WriteLine(service.CalculateFinalPrice(100)); // 90
```

- **Key Benefit**: Switch or add new “strategies” at runtime or compile time without altering the client code.

### 2.2 Observer

**Intent**

- Define a one-to-many dependency so that when one object changes state, all its dependents are notified and updated automatically.

**Scenario**

- You want multiple components to stay in sync with changes in a particular “subject” or data source (e.g., UI update on data change, event-driven design).

**Example**

```csharp
public interface IObserver
{
    void Update(string message);
}

public class Subject
{
    private readonly List<IObserver> _observers = new List<IObserver>();

    public void Attach(IObserver observer) => _observers.Add(observer);
    public void Detach(IObserver observer) => _observers.Remove(observer);

    public void Notify(string message)
    {
        foreach (var observer in _observers)
            observer.Update(message);
    }
}

public class ConcreteObserver : IObserver
{
    public void Update(string message)
    {
        Console.WriteLine($"Observer received: {message}");
    }
}

// Usage
var subject = new Subject();
var obs1 = new ConcreteObserver();
var obs2 = new ConcreteObserver();

subject.Attach(obs1);
subject.Attach(obs2);

subject.Notify("Hello observers!"); // Both obs1 and obs2 get the message
```

- **Key Benefit**: Loose coupling between the subject and observers; you can add or remove observers at will.

### 2.3 Decorator

**Intent**

- Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

**Scenario**

- You have a core component (e.g., a `Stream` in .NET) and you need to add features (e.g., buffering, compression) without rewriting or heavily modifying the original.

**Example**

```csharp
public interface IMessage
{
    string GetContent();
}

public class TextMessage : IMessage
{
    private string _text;

    public TextMessage(string text) => _text = text;
    public string GetContent() => _text;
}

// Decorator
public class Base64Encoder : IMessage
{
    private readonly IMessage _message;

    public Base64Encoder(IMessage message)
    {
        _message = message;
    }

    public string GetContent()
    {
        var plainContent = _message.GetContent();
        var bytes = Encoding.UTF8.GetBytes(plainContent);
        return Convert.ToBase64String(bytes);
    }
}

// Usage
IMessage message = new TextMessage("Hello, Decorator!");
IMessage encoded = new Base64Encoder(message);
Console.WriteLine(encoded.GetContent());
```

- **Key Benefit**: You can stack multiple decorators to layer on different behaviors without changing the original `TextMessage` class.

---

## 3. Repository and Unit of Work in Enterprise Applications

### 3.1 Repository Pattern

**Intent**

- Mediate between the domain and data mapping layers using a collection-like interface for accessing domain objects.

**Scenario**

- In large systems, you want to abstract data access (e.g., EF Core, Dapper, or raw SQL) so that the domain layer doesn’t deal with low-level persistence details.

**Example**

```csharp
public interface IOrderRepository
{
    Order GetById(int id);
    void Add(Order order);
    void Remove(Order order);
    IEnumerable<Order> GetAll();
}

public class OrderRepository : IOrderRepository
{
    private readonly DbContext _context;
    public OrderRepository(DbContext context) => _context = context;

    public Order GetById(int id) => _context.Orders.Find(id);
    public void Add(Order order) => _context.Orders.Add(order);
    public void Remove(Order order) => _context.Orders.Remove(order);
    public IEnumerable<Order> GetAll() => _context.Orders.ToList();
}
```

- **Key Benefit**: You isolate data access logic, making it easy to swap EF with another ORM or mock in tests.

### 3.2 Unit of Work Pattern

**Intent**

- Maintain a list of objects affected by a business transaction and coordinate the writing out of changes and the resolution of concurrency issues.

**Scenario**

- When you have multiple repositories working together in a single business operation, you want to commit or roll back changes as one atomic action.

**Example**

```csharp
public interface IUnitOfWork : IDisposable
{
    IOrderRepository Orders { get; }
    ICustomerRepository Customers { get; }
    int Complete(); // commits changes
}

public class UnitOfWork : IUnitOfWork
{
    private readonly DbContext _context;
    public IOrderRepository Orders { get; }
    public ICustomerRepository Customers { get; }

    public UnitOfWork(DbContext context,
                      IOrderRepository orderRepo,
                      ICustomerRepository customerRepo)
    {
        _context = context;
        Orders = orderRepo;
        Customers = customerRepo;
    }

    public int Complete() => _context.SaveChanges();

    public void Dispose() => _context.Dispose();
}

// Usage
using (var uow = new UnitOfWork(new MyDbContext(),
                                new OrderRepository(),
                                new CustomerRepository()))
{
    var order = uow.Orders.GetById(1);
    order.Status = "Shipped";
    uow.Orders.Add(order);

    uow.Complete(); // transaction commits all changes
}
```

- **Key Benefit**: Central control of transactions across multiple repositories, simplifying error handling and rollback scenarios.

---

## 4. Using Patterns to Decouple Subsystems

### 4.1 Service Layer + Repository Pattern

**Why Combine Them?**

- **Repositories** handle data access; **Service Layer** coordinates higher-level operations or domain logic, calling the repositories underneath.
- **Decoupling**: The upper layers (controllers, UI, or AI modules) call the **Service Layer**, which uses the **Repository** to persist and retrieve data.

**Example**

```csharp
public class OrderService
{
    private readonly IOrderRepository _orderRepo;
    private readonly IUnitOfWork _unitOfWork;

    public OrderService(IOrderRepository orderRepo, IUnitOfWork unitOfWork)
    {
        _orderRepo = orderRepo;
        _unitOfWork = unitOfWork;
    }

    public void PlaceOrder(Order order)
    {
        _orderRepo.Add(order);
        _unitOfWork.Complete();
    }
}
```

- **Key Benefit**: UI or business logic can call `OrderService` to handle complex workflows. The domain logic remains separate from data access details.

### 4.2 Integrating with Other Patterns

- **Factories** can instantiate domain objects or services without the client knowing the specific classes.
- **Strategy** or **Decorator** can be applied within the service or repository layers to handle special behaviors (e.g., caching decorators on repository calls, discount strategies in order calculations).
- **Observer** can notify other bounded contexts or microservices (e.g., sending an event whenever a new order is placed).

---
