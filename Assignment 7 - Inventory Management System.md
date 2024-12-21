```txt
Client Request:
"I run a store, and I need to keep track of inventory, suppliers, and sales. Each product will have details like name, category, price, stock quantity, and reorder level. Products will be supplied by multiple suppliers, and I need their details like name, contact information, and the date of the last restock.
We also have customers who make purchases, so I’d like to track their details and purchase history. Sales transactions should include the date, products purchased, quantities, and total cost. Can you also include a feature to track discounts or promotions for specific products? Finally, I’d like reports on top-selling products, low-stock items, and supplier performance."

```

### **Client Request Analysis: Store Inventory, Supplier, and Sales Management System**

---

### **1. Introduction:**

The client, a store owner, requires a comprehensive system to manage inventory, suppliers, sales, and customer information. The system should facilitate tracking of products, their categories, pricing, stock levels, and reorder points. Additionally, it must handle supplier details, customer purchases, sales transactions, discounts/promotions, and generate essential reports to aid in decision-making and operational efficiency.

---

### **2. Business Requirements:**

#### **2.1 Inventory Management:**

- **Product Details:** The system must store detailed information about each product, including:
  - **Name**
  - **Category** (e.g., Electronics, Groceries, Apparel)
  - **Price**
  - **Stock Quantity**
  - **Reorder Level** (minimum stock before reordering is necessary)
- **Stock Tracking:** Real-time tracking of stock levels to ensure adequate inventory and prevent stockouts or overstocking.
- **Reorder Alerts:** Automated alerts when stock quantities reach the reorder level to prompt timely restocking.

#### **2.2 Supplier Management:**

- **Supplier Details:** The system should maintain comprehensive information about suppliers, including:
  - **Name**
  - **Contact Information** (phone number, email, address)
  - **Date of Last Restock** (to monitor supply frequency and reliability)
- **Supplier-Product Relationship:** Support for a **many-to-many** relationship where each product can have multiple suppliers and each supplier can supply multiple products.

#### **2.3 Customer Management:**

- **Customer Details:** The system must store customer information, including:
  - **Name**
  - **Contact Information** (phone number, email, address)
  - **Purchase History** (records of past purchases for personalized service and marketing)
- **Loyalty Programs:** (Optional) Track customer loyalty points or rewards based on purchase history.

#### **2.4 Sales Management:**

- **Sales Transactions:** Each sale should capture:
  - **Date of Purchase**
  - **Products Purchased**
  - **Quantities**
  - **Total Cost**
- **Discounts and Promotions:** Ability to apply and track discounts or promotional offers on specific products or during specific periods.

#### **2.5 Reporting:**

- **Top-Selling Products:** Identify and analyze best-performing products based on sales volume or revenue.
- **Low-Stock Items:** Monitor products that are low in stock to prioritize restocking.
- **Supplier Performance:** Evaluate suppliers based on criteria such as delivery timeliness, product quality, and frequency of restocks.

---

### **3. Functional Requirements:**

- **CRUD Operations:** The system must allow users to Create, Read, Update, and Delete:
  - **Products:** Manage product details, categories, pricing, stock levels, and reorder points.
  - **Suppliers:** Manage supplier information and their associated products.
  - **Customers:** Manage customer profiles and track purchase history.
  - **Sales Transactions:** Record and manage sales data, including discounts and promotions.
- **Inventory Management:**
  - **Real-Time Stock Updates:** Automatically update stock levels upon sales or restocking.
  - **Reorder Alerts:** Generate notifications when stock reaches reorder levels.
- **Supplier Management:**
  - **Supplier-Product Linking:** Associate multiple suppliers with each product.
  - **Restock Tracking:** Log dates of last restocks for each supplier-product pair.
- **Customer Management:**
  - **Purchase History Tracking:** Maintain detailed records of each customer's past purchases.
  - **Preference Management:** (Optional) Track customer preferences for targeted marketing.
- **Sales Management:**
  - **Discount/Promotion Handling:** Apply discounts or promotions to specific products or orders and track their usage.
- **Reporting:**
  - **Generate Reports:** Create reports on top-selling products, low-stock items, and supplier performance with filtering options (e.g., date ranges).
  - **Export Options:** Allow exporting reports in various formats (e.g., PDF, Excel).

---

### **4. Data Modeling (ERD):**

- **Products Table:**
  - **Fields:** Product ID, Name, Category ID, Price, Stock Quantity, Reorder Level.
- **Categories Table:**
  - **Fields:** Category ID, Category Name.
- **Suppliers Table:**
  - **Fields:** Supplier ID, Name, Contact Information, Date of Last Restock.
- **Suppliers_Products Table:**
  - **Fields:** Supplier ID, Product ID (to establish a many-to-many relationship).
- **Customers Table:**
  - **Fields:** Customer ID, Name, Contact Information.
- **Purchase_History Table:**
  - **Fields:** Purchase ID, Customer ID, Product ID, Quantity, Date of Purchase, Total Cost.
- **Sales_Transactions Table:**
  - **Fields:** Transaction ID, Date, Customer ID, Total Cost, Discount Applied.
- **Discounts_Promotions Table:**
  - **Fields:** Discount ID, Product ID, Discount Type, Discount Value, Start Date, End Date.
- **Reports Table:**
  - **Virtual/Table Queries:** For generating top-selling products, low-stock items, and supplier performance.

---

### **5. Non-Functional Requirements:**

- **Performance:**
  - The system should handle a large number of products, suppliers, customers, and transactions without performance degradation.
  - Quick response times for inventory updates and report generation.
- **Security:**
  - Protect sensitive data such as customer contact information and sales transactions.
  - Implement role-based access control to restrict functionalities based on user roles (e.g., admin, sales staff).
- **Scalability:**
  - Ability to scale with the growth of the store, accommodating more products, suppliers, and customers.
- **Usability:**
  - Intuitive user interface for ease of use by staff with varying technical expertise.
  - Mobile-friendly design (optional) for access on tablets or smartphones.
- **Data Integrity:**
  - Ensure accurate and consistent data across all modules, especially in inventory and sales tracking.
- **Backup and Recovery:**
  - Regular data backups and a robust recovery plan to prevent data loss.

---

### **6. User Stories and Use Cases:**

- **User Story 1:** As a **store manager**, I want to add new products with their details and assign multiple suppliers, so that I can manage inventory effectively.
- **User Story 2:** As a **sales associate**, I want to record sales transactions, including applied discounts, so that I can track daily revenue accurately.
- **User Story 3:** As a **warehouse staff member**, I want to receive alerts when stock levels are low, so that I can reorder products in a timely manner.
- **User Story 4:** As a **business analyst**, I want to generate reports on top-selling products and supplier performance, so that I can make informed purchasing and marketing decisions.
- **Use Case:** **Process a Sale:** A customer selects products to purchase. The sales associate records the sale, applies any applicable discounts, updates the stock levels, and generates a sales transaction record. The system updates inventory and logs the purchase in the customer's purchase history.

---

### **7. Risk Assessment:**

- **Data Security Risks:** Unauthorized access to sensitive customer and sales data could lead to data breaches. Mitigation includes implementing strong authentication mechanisms and encryption.
- **System Downtime:** Downtime can disrupt sales and inventory management. Mitigation involves using reliable hosting services and implementing failover strategies.
- **Data Integrity Issues:** Inaccurate inventory or sales data can lead to operational inefficiencies. Mitigation includes implementing validation checks and regular audits.
- **Scalability Challenges:** As the store grows, the system may face performance issues if not designed to scale. Mitigation involves choosing scalable technologies and architecture.
- **User Adoption:** Staff may resist adopting the new system, leading to underutilization. Mitigation includes comprehensive training and creating user-friendly interfaces.

---

### **8. Final Deliverables:**

- **Business Requirements Document (BRD):** Detailed documentation outlining all business needs, system functionalities, and constraints for inventory, supplier, and sales management.
- **Functional Specification Document (FSD):** Comprehensive guide detailing system features, workflows, user roles, and interactions.
- **Entity-Relationship Diagram (ERD):** Visual representation of the database structure, illustrating entities and their relationships.
- **Wireframes/UI Designs:** Mockups of the user interface for different user roles, focusing on ease of navigation and efficiency in task execution.
- **Test Cases:** Detailed test scenarios and scripts to validate each system functionality, ensuring reliability and performance.
- **Training Materials:** Guides and tutorials to help staff understand and effectively use the new system.

---

### ERD for Store Inventory, Supplier, and Sales Management System

#### **Entities and Relationships**

1. **Products**  
   Fields:

   - Product_ID (PK)
   - Name
   - Category_ID (FK)
   - Price
   - Stock_Quantity
   - Reorder*Level  
     \_Relationships*:
   - **Product Category**: A product belongs to a category (1:1 relationship with Categories).
   - **Supplier-Product**: Many-to-many relationship with Suppliers (through Suppliers_Products table).
   - **Sales Transaction**: A product can appear in multiple sales transactions.

2. **Categories**  
   Fields:

   - Category_ID (PK)
   - Category*Name  
     \_Relationships*:
   - **Products**: One category can have many products (1:many relationship with Products).

3. **Suppliers**  
   Fields:

   - Supplier_ID (PK)
   - Name
   - Contact_Information
   - Date*of_Last_Restock  
     \_Relationships*:
   - **Supplier-Product**: Many-to-many relationship with Products (through Suppliers_Products table).
   - **Purchase History**: Suppliers provide products to customers via sales transactions.

4. **Suppliers_Products**  
   Fields:

   - Supplier_ID (FK)
   - Product*ID (FK)  
     \_Relationships*:
   - **Suppliers**: A product can be supplied by multiple suppliers (many-to-many relationship with Suppliers).
   - **Products**: A supplier can provide multiple products (many-to-many relationship with Products).

5. **Customers**  
   Fields:

   - Customer_ID (PK)
   - Name
   - Contact*Information  
     \_Relationships*:
   - **Purchase History**: A customer can make multiple purchases (1:many relationship with Purchase_History).
   - **Sales Transactions**: A customer can make multiple sales transactions (1:many relationship with Sales_Transactions).

6. **Purchase History**  
   Fields:

   - Purchase_ID (PK)
   - Customer_ID (FK)
   - Product_ID (FK)
   - Quantity
   - Date_of_Purchase
   - Total*Cost  
     \_Relationships*:
   - **Customer**: Each purchase record links to one customer (many-to-one relationship with Customers).
   - **Product**: Each purchase record links to one product (many-to-one relationship with Products).

7. **Sales Transactions**  
   Fields:

   - Transaction_ID (PK)
   - Date
   - Customer_ID (FK)
   - Total_Cost
   - Discount*Applied  
     \_Relationships*:
   - **Customer**: A sale is associated with one customer (many-to-one relationship with Customers).
   - **Products**: Each sale can include multiple products (many-to-many relationship, modeled by a junction table or line item).
   - **Discounts/Promotions**: Discounts applied during the transaction are tracked.

8. **Discounts/Promotions**  
   Fields:

   - Discount_ID (PK)
   - Product_ID (FK)
   - Discount_Type
   - Discount_Value
   - Start_Date
   - End*Date  
     \_Relationships*:
   - **Product**: A discount is applied to a specific product (many-to-one relationship with Products).
   - **Sales Transactions**: Discounts can be applied to sales transactions.

9. **Reports** (Virtual or Query-Driven)  
   _Relationships_:
   - **Products**: Reports can pull data from products, like sales volume, top-selling products, and low-stock items.
   - **Sales Transactions**: Reports pull data on revenue and discounts.

#### **Key Relationships and Corner Cases**

- **Products-Suppliers**: Many-to-many relationship ensures flexibility in product sourcing from multiple suppliers.
- **Sales Transactions**: Tracks product-level sales with discounts. If a product is discounted, it’s tracked in the Sales_Transactions table.
- **Reorder Alerts**: Stock quantities are monitored in real-time, triggering reorder notifications.
- **Purchase History**: Provides detailed tracking of customer purchases for personalized service.
- **Supplier Restocks**: Logs are maintained to track when suppliers last restocked, ensuring timely supply chain management.

#### **ERD Diagram Overview** (Entities and their relationships):

- **Products** (PK: Product_ID) ↔ **Categories** (PK: Category_ID)
- **Suppliers** (PK: Supplier_ID) ↔ **Suppliers_Products** ↔ **Products** (FK: Product_ID)
- **Customers** (PK: Customer_ID) ↔ **Purchase History** ↔ **Products** (FK: Product_ID)
- **Sales Transactions** (PK: Transaction_ID) ↔ **Customers** (FK: Customer_ID)
- **Discounts/Promotions** (PK: Discount_ID) ↔ **Products** (FK: Product_ID) ↔ **Sales Transactions**
- **Reports** (Query-Driven from Products, Sales Transactions, Suppliers)

---

```mermaid

erDiagram
    PRODUCTS {
        int Product_ID PK
        string Name
        int Category_ID FK
        float Price
        int Stock_Quantity
        int Reorder_Level
    }
    CATEGORIES {
        int Category_ID PK
        string Category_Name
    }
    SUPPLIERS {
        int Supplier_ID PK
        string Name
        string Contact_Information
        date Date_of_Last_Restock
    }
    SUPPLIERS_PRODUCTS {
        int Supplier_ID FK
        int Product_ID FK
    }
    CUSTOMERS {
        int Customer_ID PK
        string Name
        string Contact_Information
    }
    PURCHASE_HISTORY {
        int Purchase_ID PK
        int Customer_ID FK
        int Product_ID FK
        int Quantity
        date Date_of_Purchase
        float Total_Cost
    }
    SALES_TRANSACTIONS {
        int Transaction_ID PK
        date Date
        int Customer_ID FK
        float Total_Cost
        float Discount_Applied
    }
    DISCOUNTS_PROMOTIONS {
        int Discount_ID PK
        int Product_ID FK
        string Discount_Type
        float Discount_Value
        date Start_Date
        date End_Date
    }

    PRODUCTS ||--o| CATEGORIES : "belongs to"
    SUPPLIERS ||--o| SUPPLIERS_PRODUCTS : "provides"
    PRODUCTS ||--o| SUPPLIERS_PRODUCTS : "supplied by"
    CUSTOMERS ||--o| PURCHASE_HISTORY : "makes"
    PRODUCTS ||--o| PURCHASE_HISTORY : "purchased"
    CUSTOMERS ||--o| SALES_TRANSACTIONS : "makes"
    PRODUCTS ||--o| SALES_TRANSACTIONS : "sold in"
    PRODUCTS ||--o| DISCOUNTS_PROMOTIONS : "has discount"
    SALES_TRANSACTIONS ||--o| DISCOUNTS_PROMOTIONS : "applies"

```

---

### SQL Queries for Store Inventory, Supplier, and Sales Management System

Below are the SQL queries based on your ERD and relationships. These queries include table creation, handling relationships, and managing corner cases.

---

### 1. **Table Creation Queries**

#### **Products Table**

```sql
CREATE TABLE Products (
    Product_ID INT PRIMARY KEY,
    Name VARCHAR(255),
    Category_ID INT,
    Price DECIMAL(10, 2),
    Stock_Quantity INT,
    ReorderLevel INT,
    FOREIGN KEY (Category_ID) REFERENCES Categories(Category_ID)
);
```

#### **Categories Table**

```sql
CREATE TABLE Categories (
    Category_ID INT PRIMARY KEY,
    CategoryName VARCHAR(255)
);
```

#### **Suppliers Table**

```sql
CREATE TABLE Suppliers (
    Supplier_ID INT PRIMARY KEY,
    Name VARCHAR(255),
    Contact_Information TEXT,
    Dateof_Last_Restock DATE
);
```

#### **Suppliers_Products Table (Many-to-Many Relationship)**

```sql
CREATE TABLE Suppliers_Products (
    Supplier_ID INT,
    Product_ID INT,
    PRIMARY KEY (Supplier_ID, Product_ID),
    FOREIGN KEY (Supplier_ID) REFERENCES Suppliers(Supplier_ID),
    FOREIGN KEY (Product_ID) REFERENCES Products(Product_ID)
);
```

#### **Customers Table**

```sql
CREATE TABLE Customers (
    Customer_ID INT PRIMARY KEY,
    Name VARCHAR(255),
    Contact_Information TEXT
);
```

#### **Purchase History Table (Links Customers and Products)**

```sql
CREATE TABLE Purchase_History (
    Purchase_ID INT PRIMARY KEY,
    Customer_ID INT,
    Product_ID INT,
    Quantity INT,
    Date_of_Purchase DATE,
    TotalCost DECIMAL(10, 2),
    FOREIGN KEY (Customer_ID) REFERENCES Customers(Customer_ID),
    FOREIGN KEY (Product_ID) REFERENCES Products(Product_ID)
);
```

#### **Sales Transactions Table**

```sql
CREATE TABLE Sales_Transactions (
    Transaction_ID INT PRIMARY KEY,
    Date DATE,
    Customer_ID INT,
    Total_Cost DECIMAL(10, 2),
    DiscountApplied DECIMAL(10, 2),
    FOREIGN KEY (Customer_ID) REFERENCES Customers(Customer_ID)
);
```

#### **Discounts/Promotions Table**

```sql
CREATE TABLE Discounts (
    Discount_ID INT PRIMARY KEY,
    Product_ID INT,
    Discount_Type VARCHAR(50),
    Discount_Value DECIMAL(10, 2),
    Start_Date DATE,
    End_Date DATE,
    FOREIGN KEY (Product_ID) REFERENCES Products(Product_ID)
);
```

#### **Reports Table (Query-Driven, for storing metadata)**

```sql
CREATE TABLE Reports (
    ReportID INT PRIMARY KEY,
    ReportType VARCHAR(50),
    DateGenerated DATE,
    ReportData TEXT
);
```

---

### 2. **Handling Corner Cases**

#### **1. Room Availability and Stock Alerts**

To track stock levels and trigger alerts for products that fall below the reorder level:

```sql
-- Check products below reorder level
SELECT Product_ID, Name, Stock_Quantity, ReorderLevel
FROM Products
WHERE Stock_Quantity <= ReorderLevel;
```

#### **2. Handling Many-to-Many Relationships (Suppliers and Products)**

Inserting or querying a product-supplier relationship:

```sql
-- Insert a relationship between a product and a supplier
INSERT INTO Suppliers_Products (Supplier_ID, Product_ID)
VALUES (1, 101);

-- Query all products supplied by a specific supplier
SELECT p.Name
FROM Products p
JOIN Suppliers_Products sp ON p.Product_ID = sp.Product_ID
WHERE sp.Supplier_ID = 1;
```

#### **3. Handling Sales Transactions and Discounts**

Tracking sales transactions and applying discounts to products:

```sql
-- Insert a sale transaction for a customer
INSERT INTO Sales_Transactions (Transaction_ID, Date, Customer_ID, Total_Cost, DiscountApplied)
VALUES (1, '2024-12-05', 2, 500.00, 50.00);

-- Apply discounts to products during sales transaction
UPDATE Sales_Transactions
SET Total_Cost = Total_Cost - DiscountApplied
WHERE Transaction_ID = 1;

-- Query sales transactions including discounts
SELECT st.Transaction_ID, st.Total_Cost, st.DiscountApplied, p.Name
FROM Sales_Transactions st
JOIN Purchase_History ph ON st.Transaction_ID = ph.Purchase_ID
JOIN Products p ON ph.Product_ID = p.Product_ID
WHERE st.Transaction_ID = 1;
```

#### **4. Handling Purchase History for Customers**

Tracking customer purchase history:

```sql
-- Query the purchase history of a customer
SELECT ph.Purchase_ID, p.Name, ph.Quantity, ph.TotalCost, ph.Date_of_Purchase
FROM Purchase_History ph
JOIN Products p ON ph.Product_ID = p.Product_ID
WHERE ph.Customer_ID = 2;

-- Calculate total purchases for a customer
SELECT SUM(ph.TotalCost) AS TotalSpent
FROM Purchase_History ph
WHERE ph.Customer_ID = 2;
```

#### **5. Supplier Restock Management**

Tracking the last restock date and ensuring timely supply chain management:

```sql
-- Query suppliers and the products they provide
SELECT s.Name, p.Name, sp.Supplier_ID, sp.Product_ID
FROM Suppliers s
JOIN Suppliers_Products sp ON s.Supplier_ID = sp.Supplier_ID
JOIN Products p ON sp.Product_ID = p.Product_ID
WHERE s.Dateof_Last_Restock < '2024-11-01';

-- Update the restock date after a supplier delivers products
UPDATE Suppliers
SET Dateof_Last_Restock = '2024-12-01'
WHERE Supplier_ID = 1;
```

---

### 3. **Report Generation Queries**

These reports can be generated dynamically using SQL, or stored in the `Reports` table.

#### **Product Sales Report (Top-Selling Products)**

```sql
SELECT p.Name, SUM(ph.Quantity) AS TotalSold
FROM Products p
JOIN Purchase_History ph ON p.Product_ID = ph.Product_ID
GROUP BY p.Name
ORDER BY TotalSold DESC;
```

#### **Revenue Report**

```sql
SELECT SUM(Total_Cost) AS TotalRevenue
FROM Sales_Transactions;
```

#### **Stock Alert Report (Low-Stock Products)**

```sql
SELECT p.Name, p.Stock_Quantity, p.ReorderLevel
FROM Products p
WHERE p.Stock_Quantity <= p.ReorderLevel;
```

#### **Discount Report**

```sql
SELECT p.Name, d.Discount_Value, d.Start_Date, d.End_Date
FROM Discounts d
JOIN Products p ON d.Product_ID = p.Product_ID;
```

---

## OOP Representation:

---

## 1. Data Models

### 1.1 Category

Represents product categories (e.g., Electronics, Groceries, Apparel).

```csharp
public class Category
{
    public int Id { get; set; }
    public string Name { get; set; }  // e.g., "Electronics", "Groceries"

    // One-to-many: A category has multiple products
    public List<Product> Products { get; set; } = new List<Product>();

    public Category(int id, string name)
    {
        Id = id;
        Name = name;
    }

    public override string ToString()
    {
        return $"{Name} (Category ID: {Id})";
    }
}
```

### 1.2 Product

Stores product details, including stock levels and reorder points.  
Many-to-many relationship with `Supplier` (a product can have multiple suppliers, and a supplier can provide multiple products).

```csharp
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public Category Category { get; set; }
    public decimal Price { get; set; }
    public int StockQuantity { get; set; }
    public int ReorderLevel { get; set; }    // threshold for low stock alerts

    // Many-to-many: A product can be supplied by multiple suppliers
    public List<Supplier> Suppliers { get; set; } = new List<Supplier>();

    public Product(int id, string name, Category category, decimal price, int stockQuantity, int reorderLevel)
    {
        Id = id;
        Name = name;
        Category = category;
        Price = price;
        StockQuantity = stockQuantity;
        ReorderLevel = reorderLevel;
    }

    public override string ToString()
    {
        return $"{Name} (ID: {Id}), Price: {Price:C}, Stock: {StockQuantity}, Reorder Level: {ReorderLevel}";
    }
}
```

### 1.3 Supplier

Stores supplier information.  
Tracks date of last restock and can link to multiple products.

```csharp
public class Supplier
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string ContactInfo { get; set; }   // e.g., phone, email, address
    public DateTime? DateOfLastRestock { get; set; }

    // Many-to-many: A supplier can supply multiple products
    public List<Product> ProductsSupplied { get; set; } = new List<Product>();

    public Supplier(int id, string name, string contactInfo)
    {
        Id = id;
        Name = name;
        ContactInfo = contactInfo;
    }

    public override string ToString()
    {
        return $"{Name} (ID: {Id}), Contact: {ContactInfo}, Last Restock: {DateOfLastRestock?.ToShortDateString() ?? "N/A"}";
    }
}
```

### 1.4 Customer

Stores customer details and purchase history.  
(Purchase history can be retrieved from a separate repository or stored as a list of transactions.)

```csharp
public class Customer
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string ContactInfo { get; set; }   // e.g., phone, email, address

    // Optionally track loyalty points, preferences, etc.

    public Customer(int id, string name, string contactInfo)
    {
        Id = id;
        Name = name;
        ContactInfo = contactInfo;
    }

    public override string ToString()
    {
        return $"{Name} (ID: {Id}), Contact: {ContactInfo}";
    }
}
```

### 1.5 Discount/Promotion

Represents a discount or promotion that can be applied to a **product** within a date range.

```csharp
public class Discount
{
    public int Id { get; set; }
    public Product Product { get; set; } // which product is discounted
    public string DiscountType { get; set; }  // e.g., "Percentage", "Flat"
    public decimal DiscountValue { get; set; } // e.g., 10% or $5 off
    public DateTime StartDate { get; set; }
    public DateTime EndDate { get; set; }

    public Discount(int id, Product product, string discountType, decimal discountValue, DateTime startDate, DateTime endDate)
    {
        Id = id;
        Product = product;
        DiscountType = discountType;
        DiscountValue = discountValue;
        StartDate = startDate;
        EndDate = endDate;
    }

    public override string ToString()
    {
        return $"Discount #{Id}, {DiscountType}={DiscountValue}, Valid: {StartDate.ToShortDateString()} - {EndDate.ToShortDateString()} on {Product.Name}";
    }
}
```

### 1.6 SalesTransaction

Represents a sales transaction, linking a `Customer` to purchased products.  
This can be expanded to include partial payments, multiple payment methods, etc.

```csharp
public class SalesTransaction
{
    public int Id { get; set; }
    public DateTime DateOfPurchase { get; set; }
    public Customer Customer { get; set; }
    public decimal TotalCost { get; set; }    // final cost after discounts
    public decimal DiscountApplied { get; set; }

    // A list of items purchased: (Product, Quantity)
    public List<(Product item, int quantity)> PurchasedItems { get; set; }
        = new List<(Product item, int quantity)>();

    public SalesTransaction(int id, Customer customer)
    {
        Id = id;
        Customer = customer;
        DateOfPurchase = DateTime.Now;
        TotalCost = 0m;
        DiscountApplied = 0m;
    }

    public override string ToString()
    {
        return $"Transaction #{Id}, Date: {DateOfPurchase}, Customer: {Customer.Name}, Total: {TotalCost:C}, Discount: {DiscountApplied:C}";
    }
}
```

---

## 2. Repositories (In-Memory)

We’ll define a generic `IRepository<T>` interface for CRUD operations, then create a `GenericRepository<T>` implementation.

```csharp
public interface IRepository<T>
{
    void Add(T entity);
    T GetById(int id);
    IEnumerable<T> GetAll();
    void Update(T entity);
    void Delete(int id);
}

public class GenericRepository<T> : IRepository<T>
{
    private readonly List<T> _items = new List<T>();

    public void Add(T entity)
    {
        _items.Add(entity);
    }

    public T GetById(int id)
    {
        // Reflection approach: get property named "Id".
        return _items.FirstOrDefault(x =>
            (int)x.GetType().GetProperty("Id").GetValue(x) == id
        );
    }

    public IEnumerable<T> GetAll()
    {
        return _items;
    }

    public void Update(T entity)
    {
        var entityId = (int)entity.GetType().GetProperty("Id").GetValue(entity);
        var existing = GetById(entityId);
        if (existing != null)
        {
            _items.Remove(existing);
            _items.Add(entity);
        }
    }

    public void Delete(int id)
    {
        var existing = GetById(id);
        if (existing != null) _items.Remove(existing);
    }
}
```

_(We instantiate this repository for `Product`, `Category`, `Supplier`, `Customer`, `Discount`, `SalesTransaction`, etc.)_

---

## 3. Core Service: `StoreService`

The `StoreService` orchestrates main business operations:

- **Inventory management** (stock updates, reorder alerts)
- **Supplier linking** (associate multiple suppliers with a product)
- **Sales** (process transactions, apply discounts)
- **Reporting** (top-selling products, low-stock items, supplier performance)

```csharp
public class StoreService
{
    private readonly IRepository<Category> _categoryRepo;
    private readonly IRepository<Product> _productRepo;
    private readonly IRepository<Supplier> _supplierRepo;
    private readonly IRepository<Customer> _customerRepo;
    private readonly IRepository<Discount> _discountRepo;
    private readonly IRepository<SalesTransaction> _salesRepo;

    public StoreService(
        IRepository<Category> categoryRepo,
        IRepository<Product> productRepo,
        IRepository<Supplier> supplierRepo,
        IRepository<Customer> customerRepo,
        IRepository<Discount> discountRepo,
        IRepository<SalesTransaction> salesRepo)
    {
        _categoryRepo = categoryRepo;
        _productRepo = productRepo;
        _supplierRepo = supplierRepo;
        _customerRepo = customerRepo;
        _discountRepo = discountRepo;
        _salesRepo = salesRepo;
    }

    // ------------------------------
    // Inventory Management
    // ------------------------------

    /// <summary>
    /// Adjusts stock for a product (e.g., when restocking).
    /// </summary>
    public void UpdateProductStock(int productId, int quantityChange)
    {
        var product = _productRepo.GetById(productId);
        if (product == null) throw new Exception("Product not found.");

        product.StockQuantity += quantityChange;
        _productRepo.Update(product);

        Console.WriteLine($"Stock updated for {product.Name}. New quantity: {product.StockQuantity}");
    }

    /// <summary>
    /// Returns all products whose stock is at or below the reorder level.
    /// </summary>
    public IEnumerable<Product> GetLowStockProducts()
    {
        return _productRepo.GetAll()
            .Where(p => p.StockQuantity <= p.ReorderLevel);
    }

    // ------------------------------
    // Supplier Management
    // ------------------------------

    /// <summary>
    /// Links a supplier to a product (many-to-many relationship).
    /// Optionally set the date of last restock, etc.
    /// </summary>
    public void LinkSupplierToProduct(int supplierId, int productId)
    {
        var supplier = _supplierRepo.GetById(supplierId);
        if (supplier == null) throw new Exception("Supplier not found.");

        var product = _productRepo.GetById(productId);
        if (product == null) throw new Exception("Product not found.");

        if (!supplier.ProductsSupplied.Contains(product))
            supplier.ProductsSupplied.Add(product);
        if (!product.Suppliers.Contains(supplier))
            product.Suppliers.Add(supplier);

        _supplierRepo.Update(supplier);
        _productRepo.Update(product);

        Console.WriteLine($"Linked supplier '{supplier.Name}' with product '{product.Name}'.");
    }

    /// <summary>
    /// Updates the last restock date for a supplier.
    /// </summary>
    public void UpdateSupplierRestockDate(int supplierId, DateTime restockDate)
    {
        var supplier = _supplierRepo.GetById(supplierId);
        if (supplier == null) throw new Exception("Supplier not found.");

        supplier.DateOfLastRestock = restockDate;
        _supplierRepo.Update(supplier);

        Console.WriteLine($"Supplier '{supplier.Name}' last restock updated to {restockDate.ToShortDateString()}.");
    }

    // ------------------------------
    // Sales & Discounts
    // ------------------------------

    /// <summary>
    /// Processes a sale for a given customer, applying any active discounts if applicable.
    /// </summary>
    public SalesTransaction ProcessSale(int customerId, List<(int productId, int quantity)> cartItems)
    {
        var customer = _customerRepo.GetById(customerId);
        if (customer == null) throw new Exception("Customer not found.");

        var transaction = new SalesTransaction(GenerateTransactionId(), customer);

        // Calculate total cost, apply discounts if any are active
        decimal subtotal = 0m;
        decimal discountApplied = 0m;

        foreach (var (productId, quantity) in cartItems)
        {
            var product = _productRepo.GetById(productId);
            if (product == null) throw new Exception($"Product with ID {productId} not found.");
            if (product.StockQuantity < quantity)
                throw new Exception($"Insufficient stock for product '{product.Name}'.");

            // Decrease stock
            product.StockQuantity -= quantity;
            _productRepo.Update(product);

            // Check if there's an active discount for this product
            var activeDiscount = _discountRepo.GetAll()
                .FirstOrDefault(d =>
                    d.Product.Id == product.Id &&
                    DateTime.Now >= d.StartDate &&
                    DateTime.Now <= d.EndDate
                );

            decimal itemCost = product.Price;
            if (activeDiscount != null)
            {
                if (activeDiscount.DiscountType == "Percentage")
                {
                    var amountOff = product.Price * (activeDiscount.DiscountValue / 100m);
                    itemCost -= amountOff;
                    discountApplied += amountOff * quantity;
                }
                else if (activeDiscount.DiscountType == "Flat")
                {
                    itemCost -= activeDiscount.DiscountValue;
                    discountApplied += activeDiscount.DiscountValue * quantity;
                }
            }

            var lineTotal = itemCost * quantity;
            subtotal += lineTotal;

            // Add to transaction items
            transaction.PurchasedItems.Add((product, quantity));
        }

        transaction.TotalCost = subtotal;
        transaction.DiscountApplied = discountApplied;

        _salesRepo.Add(transaction);

        Console.WriteLine($"Sale processed: {transaction}");
        return transaction;
    }

    // ------------------------------
    // Reporting
    // ------------------------------

    /// <summary>
    /// Returns top-selling products by total quantity sold, or by revenue, if needed.
    /// </summary>
    public List<(Product product, int quantitySold)> GetTopSellingProducts(int topN = 5)
    {
        // We'll track how many units each product sold across transactions.
        var productSales = new Dictionary<Product, int>();

        foreach (var sale in _salesRepo.GetAll())
        {
            foreach (var (item, qty) in sale.PurchasedItems)
            {
                if (!productSales.ContainsKey(item))
                {
                    productSales[item] = 0;
                }
                productSales[item] += qty;
            }
        }

        return productSales
            .OrderByDescending(ps => ps.Value)
            .Take(topN)
            .Select(ps => (ps.Key, ps.Value))
            .ToList();
    }

    /// <summary>
    /// Reports on supplier performance.
    /// For demonstration, we might just list suppliers who restocked recently or compare restock dates.
    /// </summary>
    public void PrintSupplierPerformance()
    {
        var allSuppliers = _supplierRepo.GetAll()
            .OrderByDescending(s => s.DateOfLastRestock);
        Console.WriteLine("--- Supplier Performance (Recent Restocks) ---");
        foreach (var sup in allSuppliers)
        {
            Console.WriteLine(sup);
        }
    }

    // ------------------------------
    // Helper ID Generator
    // ------------------------------

    private int GenerateTransactionId()
    {
        return new Random().Next(10000, 99999);
    }
}
```

---

## 4. Demonstration / Usage

```csharp
public class Program
{
    public static void Main()
    {
        // Create in-memory repositories
        var categoryRepo = new GenericRepository<Category>();
        var productRepo = new GenericRepository<Product>();
        var supplierRepo = new GenericRepository<Supplier>();
        var customerRepo = new GenericRepository<Customer>();
        var discountRepo = new GenericRepository<Discount>();
        var salesRepo = new GenericRepository<SalesTransaction>();

        // Create the StoreService
        var storeService = new StoreService(
            categoryRepo,
            productRepo,
            supplierRepo,
            customerRepo,
            discountRepo,
            salesRepo
        );

        // 1) Seed initial data
        SeedData(categoryRepo, productRepo, supplierRepo, customerRepo, discountRepo);

        // 2) Link a supplier to a product
        storeService.LinkSupplierToProduct(supplierId: 1, productId: 100);

        // 3) Process a sale
        var cartItems = new List<(int productId, int quantity)>
        {
            (100, 2),  // 2 x "Laptop"
            (101, 3)   // 3 x "Smartphone"
        };
        var transaction = storeService.ProcessSale(customerId: 1, cartItems);

        // 4) Check for low stock items
        Console.WriteLine("\n--- Low Stock Items ---");
        var lowStock = storeService.GetLowStockProducts();
        foreach (var ls in lowStock)
        {
            Console.WriteLine(ls);
        }

        // 5) Generate top-selling products report
        Console.WriteLine("\n--- Top-Selling Products ---");
        var topSelling = storeService.GetTopSellingProducts();
        foreach (var (product, qty) in topSelling)
        {
            Console.WriteLine($"{product.Name} sold {qty} units.");
        }

        // 6) Supplier performance
        Console.WriteLine("\n--- Supplier Performance ---");
        storeService.PrintSupplierPerformance();
    }

    private static void SeedData(
        IRepository<Category> categoryRepo,
        IRepository<Product> productRepo,
        IRepository<Supplier> supplierRepo,
        IRepository<Customer> customerRepo,
        IRepository<Discount> discountRepo)
    {
        // Categories
        var catElectronics = new Category(10, "Electronics");
        var catGroceries = new Category(11, "Groceries");
        categoryRepo.Add(catElectronics);
        categoryRepo.Add(catGroceries);

        // Products
        var product1 = new Product(100, "Laptop", catElectronics, 999.99m, stockQuantity: 10, reorderLevel: 2);
        var product2 = new Product(101, "Smartphone", catElectronics, 599.99m, stockQuantity: 20, reorderLevel: 5);
        var product3 = new Product(102, "Bananas (1 lb)", catGroceries, 1.29m, stockQuantity: 50, reorderLevel: 10);
        // Link products to categories
        catElectronics.Products.Add(product1);
        catElectronics.Products.Add(product2);
        catGroceries.Products.Add(product3);

        productRepo.Add(product1);
        productRepo.Add(product2);
        productRepo.Add(product3);

        // Suppliers
        var supplier1 = new Supplier(1, "Global Tech Supplies", "555-1000, 123 Tech St");
        var supplier2 = new Supplier(2, "Fresh Foods", "555-2000, 456 Market Ave");
        supplierRepo.Add(supplier1);
        supplierRepo.Add(supplier2);

        // Customers
        var cust1 = new Customer(1, "Alice Johnson", "alice@example.com");
        var cust2 = new Customer(2, "Bob Smith", "bob@example.com");
        customerRepo.Add(cust1);
        customerRepo.Add(cust2);

        // Discounts (e.g., 10% off laptops, $50 off smartphone)
        var discount1 = new Discount(
            id: 1000,
            product: product1,
            discountType: "Percentage",
            discountValue: 10m, // 10%
            startDate: DateTime.Today.AddDays(-1),
            endDate: DateTime.Today.AddDays(7)
        );
        var discount2 = new Discount(
            id: 1001,
            product: product2,
            discountType: "Flat",
            discountValue: 50m, // $50 off
            startDate: DateTime.Today.AddDays(-2),
            endDate: DateTime.Today.AddDays(5)
        );
        discountRepo.Add(discount1);
        discountRepo.Add(discount2);
    }
}
```

### What Happens in `Main()`?

1. **Seeding Data**:

   - We create two categories (Electronics, Groceries).
   - Three products (Laptop, Smartphone, Bananas).
   - Two suppliers (Global Tech, Fresh Foods).
   - Two customers (Alice, Bob).
   - Two discounts (10% off laptops, $50 off smartphones).

2. **Link Supplier to Product**:

   - We link supplier #1 to product #100 (Laptop).

3. **Process a Sale**:

   - Customer #1 buys 2 laptops and 3 smartphones.
   - The system checks product stock, applies discounts, updates stock levels, and creates a `SalesTransaction`.

4. **Check Low Stock**:

   - We see if any products’ stock has fallen at or below their reorder level.

5. **Generate Top-Selling Products Report**:

   - Summarizes total quantities sold across all transactions.

6. **Supplier Performance**:
   - We see suppliers ordered by their last restock date (just a demo in this snippet).

---

## Final Thoughts

- **Domain Classes**: `Category`, `Product`, `Supplier`, `Customer`, `Discount`, `SalesTransaction` (and optionally more, like a `PurchaseOrder` if you track restocking in detail).
- **Relationships**:
  - **Product**–**Supplier**: many-to-many.
  - **Category**–**Product**: one-to-many.
  - **SalesTransaction**–**Product**: one-to-many within the transaction details (though it’s stored as a list of `(Product, quantity)` pairs).
- **Repository Pattern**: We used a generic in-memory approach for CRUD operations.
- **Business Logic**: Encapsulated in `StoreService`, handling real-time stock updates, discounts, supplier linkage, and reporting.
- **Reports**: Demonstrated top-selling products, low-stock items, and a simple supplier performance snapshot.

---
