```txt
Client Request:
"I own a hotel, and I need a system for managing guests, rooms, bookings, and additional services. Guests will have details like name, contact information, preferences, and booking history. Rooms will include details like room type, price per night, floor number, and availability.
Bookings should include check-in and check-out dates, payment status, and any special requests. Some bookings will include additional services like room service, spa appointments, or tours, so I need to track these separately. I’d also like to manage staff details, including their roles (e.g., housekeeping, receptionist) and schedules. Can you generate reports on room occupancy, revenue by service, and guest preferences?"

```

### **Client Request Analysis: Hotel Management System**

---

### **1. Introduction:**

The client, a hotel owner, requires a comprehensive system to manage various aspects of hotel operations. The system should help with guest management, room bookings, additional services (e.g., room service, spa), staff management, and reporting. The goal is to track guests, room availability, services provided, and generate reports for better decision-making.

---

### **2. Business Requirements:**

#### **2.1 Guest Management:**

- **Guest Details:** The system must store and manage guest information, including:
  - **Name**
  - **Contact Information** (e.g., email, phone number)
  - **Preferences** (e.g., room preferences, special requests)
  - **Booking History** (track past bookings and stay details)
- **Booking History:** Track the guest’s previous stays, services used, and any preferences noted for future visits.

#### **2.2 Room Management:**

- **Room Details:** The system must store information about rooms, including:
  - **Room Type** (e.g., Single, Double, Suite)
  - **Price per Night**
  - **Floor Number**
  - **Availability** (show whether a room is available or booked)
- **Room Availability:** Real-time updates on room availability based on bookings.

#### **2.3 Booking Management:**

- **Booking Details:** The system should manage bookings with details like:
  - **Check-in and Check-out Dates**
  - **Payment Status** (e.g., paid, pending)
  - **Special Requests** (e.g., late check-in, extra bedding)
- **Booking Status:** The system should update the status of bookings (confirmed, canceled, completed).

#### **2.4 Additional Services:**

- **Services Tracking:** Track additional services requested by guests during their stay, such as:
  - **Room Service** (e.g., food, drinks)
  - **Spa Appointments**
  - **Tour Bookings**
- **Service Details:** Store information about each service, including type, status, date, and cost.
- **Service Availability:** Track the availability of services like spa appointments or tours, ensuring no over-booking.

#### **2.5 Staff Management:**

- **Staff Details:** The system must store information on hotel staff, including:
  - **Name**
  - **Role** (e.g., Housekeeping, Receptionist, Manager)
  - **Schedule** (working hours, shifts)
- **Role-Based Access:** Different staff roles should have appropriate access to system features based on their responsibilities (e.g., receptionists can manage bookings, housekeeping can track room status).

#### **2.6 Reporting:**

- **Room Occupancy Report:** The system should generate reports on room occupancy, showing the current status of rooms and booking trends over time.
- **Revenue by Service Report:** Track revenue generated by each service, such as room service, spa, and tours.
- **Guest Preferences Report:** Generate reports on recurring guest preferences to help personalize future stays.

---

### **3. Functional Requirements:**

- **CRUD Operations:** The system should allow users to Create, Read, Update, and Delete:
  - Guest records (name, contact info, preferences)
  - Room records (type, price, availability)
  - Booking records (check-in/check-out dates, payment status)
  - Service records (type, date, price)
  - Staff records (name, role, schedule)
- **Booking Management:** Ability to create, modify, and cancel bookings. Track check-in/check-out dates and special requests.
- **Additional Services Tracking:** Ability to link services to specific bookings and guests, showing which services were used and their cost.
- **Staff Schedule Management:** Allow staff schedules to be created and updated based on shifts and roles.
- **Reports Generation:** Enable real-time generation of:
  - **Room Occupancy Reports**
  - **Revenue by Service Reports**
  - **Guest Preferences Reports**

---

### **4. Data Modeling (ERD):**

- **Guests Table:** Stores guest details such as name, contact information, and preferences.
- **Rooms Table:** Stores room details, including room type, price per night, floor number, and availability.
- **Bookings Table:** Stores booking details, including check-in/check-out dates, payment status, special requests, and linked guest ID.
- **Services Table:** Stores services provided to guests, including type (e.g., room service, spa), date, cost, and linked booking ID.
- **Staff Table:** Stores staff member details, including name, role, and work schedule.
- **Reports Table:** A virtual table or a set of queries to track occupancy rates, revenue by service, and guest preferences over time.

---

### **5. Non-Functional Requirements:**

- **Performance:** The system should efficiently handle bookings and service tracking in real-time, especially during peak times.
- **Security:** The system must ensure that guest data, especially sensitive information like contact details and payment status, is securely stored and protected.
- **Scalability:** The system should be able to scale as the hotel grows, supporting more rooms, services, and staff.
- **Usability:** The system must have an intuitive user interface that makes it easy for front desk staff and other hotel personnel to manage bookings, guests, and services.
- **Data Integrity:** Ensure the system maintains accurate and consistent data across all modules, especially in real-time updates on room availability and service bookings.

---

### **6. User Stories and Use Cases:**

- **User Story 1:** As a **guest**, I want to make a booking for a room and specify any special requests so that my stay is comfortable and tailored to my needs.
- **User Story 2:** As a **receptionist**, I want to manage bookings and check-in guests, ensuring that room availability is accurately reflected and that guests' special requests are noted.
- **User Story 3:** As a **housekeeper**, I want to see a list of rooms that need cleaning and their status (occupied or available) so that I can efficiently manage room turnover.
- **User Story 4:** As a **hotel manager**, I want to generate revenue reports by service type, allowing me to evaluate which services are most profitable.

- **Use Case:** **Booking Management:** A guest makes a booking for a room, with details like check-in and check-out dates, payment status, and any special requests. The system checks room availability, updates the booking status, and generates a report for tracking occupancy rates.

---

### **7. Risk Assessment:**

- **Data Security:** Protecting guest details and payment status is critical. The system should comply with relevant data protection regulations (e.g., GDPR).
- **System Downtime:** Any downtime, especially during high booking periods, can disrupt hotel operations. Ensure the system is hosted on a reliable platform with proper backup measures.
- **Staff Training:** Adequate training for staff is essential to ensure smooth usage, especially when managing bookings and handling guest requests.

---

### **8. Final Deliverables:**

- **Business Requirements Document (BRD):** A detailed document outlining system features and functionalities for managing guests, rooms, bookings, services, and staff.
- **Functional Specification Document (FSD):** A description of system features, including booking and service tracking, staff management, and report generation.
- **Entity-Relationship Diagram (ERD):** A visual representation of the database schema.
- **User Interface Designs:** Mockups of the system interface, focusing on ease of use for hotel staff, such as receptionists, housekeepers, and managers.
- **Test Cases:** Detailed test scenarios covering functionalities like booking management, room availability updates, and service tracking.

---

Based on the client’s requirements, here’s a structured ERD for the Hotel Management System, covering key aspects of the system and potential corner cases.

### ERD Overview:

1. **Guests Table**:

   - `GuestID` (PK)
   - `Name`
   - `Email`
   - `PhoneNumber`
   - `Preferences`
   - `BookingHistory` (One-to-Many with Bookings)

2. **Rooms Table**:

   - `RoomID` (PK)
   - `RoomType` (Single, Double, Suite)
   - `PricePerNight`
   - `FloorNumber`
   - `AvailabilityStatus` (Available, Booked)
   - `BookingID` (FK from Bookings)

3. **Bookings Table**:

   - `BookingID` (PK)
   - `GuestID` (FK from Guests)
   - `RoomID` (FK from Rooms)
   - `CheckInDate`
   - `CheckOutDate`
   - `PaymentStatus` (Paid, Pending)
   - `SpecialRequests`
   - `BookingStatus` (Confirmed, Canceled, Completed)

4. **Services Table**:

   - `ServiceID` (PK)
   - `BookingID` (FK from Bookings)
   - `ServiceType` (Room Service, Spa, Tour)
   - `ServiceDate`
   - `Cost`
   - `ServiceStatus` (Pending, Completed, Canceled)

5. **Staff Table**:

   - `StaffID` (PK)
   - `Name`
   - `Role` (Housekeeping, Receptionist, Manager)
   - `Schedule`
   - `RoleBasedAccess` (Admin, User, etc.)

6. **Reports Table** (Virtual / Derived Data):
   - `ReportID` (PK)
   - `ReportType` (Occupancy, Revenue, Guest Preferences)
   - `DateGenerated`
   - `ReportData` (Summary Data for respective reports)

### Key Relationships:

- **Guests ↔ Bookings**: One guest can have multiple bookings.
- **Rooms ↔ Bookings**: One room can be linked to many bookings (historical).
- **Bookings ↔ Services**: One booking can have multiple services linked to it.
- **Rooms ↔ Staff**: Indirect connection for room cleaning tasks (assigned by housekeeping).
- **Staff ↔ Bookings**: Staff can be responsible for managing bookings (via receptionist role).

### Corner Case Considerations:

1. **Room Availability**: Ensure the system handles room overbooking gracefully by checking availability before confirming bookings.
2. **Multiple Bookings**: Handle guest re-booking in different seasons or events with tracking of booking history and preferences.
3. **Service Availability**: Ensure that services like spa or tours aren’t overbooked by tracking availability and limiting the number of bookings for each service type.
4. **Cancellation Handling**: Ensure that canceled bookings reflect the room as available, and all linked services are also marked as canceled.
5. **Role-Based Access**: Different staff roles must have distinct access levels, so the system must handle dynamic permissions based on roles (e.g., receptionists can manage bookings, housekeepers can manage room statuses).

### Final Notes:

- The **Reports Table** could be built as a set of virtual queries or derived data, depending on how the system generates reports.
- The **Staff Schedule** should be robust to accommodate multiple shift systems and role-based permissions.

---

```mermaid

erDiagram
    GUESTS {
        int GuestID PK
        string Name
        string Email
        string PhoneNumber
        string Preferences
    }
    ROOMS {
        int RoomID PK
        string RoomType
        float PricePerNight
        int FloorNumber
        string AvailabilityStatus
    }
    BOOKINGS {
        int BookingID PK
        int GuestID FK
        int RoomID FK
        datetime CheckInDate
        datetime CheckOutDate
        string PaymentStatus
        string SpecialRequests
        string BookingStatus
    }
    SERVICES {
        int ServiceID PK
        int BookingID FK
        string ServiceType
        datetime ServiceDate
        float Cost
        string ServiceStatus
    }
    STAFF {
        int StaffID PK
        string Name
        string Role
        string Schedule
        string RoleBasedAccess
    }
    REPORTS {
        int ReportID PK
        string ReportType
        datetime DateGenerated
        string ReportData
    }

    GUESTS }|--o{ BOOKINGS : "makes"
    ROOMS }|--o{ BOOKINGS : "linked to"
    BOOKINGS }|--o{ SERVICES : "has"
    STAFF }|--o{ BOOKINGS : "manages"
    STAFF }|--o{ ROOMS : "cleans"
    REPORTS }|--o{ BOOKINGS : "summarizes"

```

---

### SQL Queries for Hotel Management System

Based on the provided ERD, I'll write the SQL queries for table creation, relationships, and corner cases handling.

---

### 1. **Table Creation Queries**

#### **Guests Table**

```sql
CREATE TABLE Guests (
    GuestID INT PRIMARY KEY,
    Name VARCHAR(255),
    Email VARCHAR(255) UNIQUE,
    PhoneNumber VARCHAR(20),
    Preferences TEXT,
    BookingHistory TEXT -- This can be a derived field or join-based if needed later
);
```

#### **Rooms Table**

```sql
CREATE TABLE Rooms (
    RoomID INT PRIMARY KEY,
    RoomType ENUM('Single', 'Double', 'Suite'),
    PricePerNight DECIMAL(10, 2),
    FloorNumber INT,
    AvailabilityStatus ENUM('Available', 'Booked'),
    BookingID INT, -- Link to Bookings for historical purposes (foreign key)
    FOREIGN KEY (BookingID) REFERENCES Bookings(BookingID)
);
```

#### **Bookings Table**

```sql
CREATE TABLE Bookings (
    BookingID INT PRIMARY KEY,
    GuestID INT,
    RoomID INT,
    CheckInDate DATETIME,
    CheckOutDate DATETIME,
    PaymentStatus ENUM('Paid', 'Pending'),
    SpecialRequests TEXT,
    BookingStatus ENUM('Confirmed', 'Canceled', 'Completed'),
    FOREIGN KEY (GuestID) REFERENCES Guests(GuestID),
    FOREIGN KEY (RoomID) REFERENCES Rooms(RoomID)
);
```

#### **Services Table**

```sql
CREATE TABLE Services (
    ServiceID INT PRIMARY KEY,
    BookingID INT,
    ServiceType ENUM('Room Service', 'Spa', 'Tour'),
    ServiceDate DATETIME,
    Cost DECIMAL(10, 2),
    ServiceStatus ENUM('Pending', 'Completed', 'Canceled'),
    FOREIGN KEY (BookingID) REFERENCES Bookings(BookingID)
);
```

#### **Staff Table**

```sql
CREATE TABLE Staff (
    StaffID INT PRIMARY KEY,
    Name VARCHAR(255),
    Role ENUM('Housekeeping', 'Receptionist', 'Manager'),
    Schedule TEXT,
    RoleBasedAccess ENUM('Admin', 'User')
);
```

#### **Reports Table (Virtual/Dervied Data)**

Reports will be generated using SQL queries or stored procedures depending on the system's reporting tools. This table could store metadata for generated reports.

```sql
CREATE TABLE Reports (
    ReportID INT PRIMARY KEY,
    ReportType ENUM('Occupancy', 'Revenue', 'Guest Preferences'),
    DateGenerated DATETIME,
    ReportData TEXT -- Stores a summary of the report data
);
```

---

### 2. **Handling Corner Cases**

#### **1. Room Availability (Preventing Overbooking)**

To prevent overbooking, we need to check if a room is available at the desired time. A booking can only be confirmed if the room is available for the check-in and check-out dates.

```sql
-- Check room availability before confirming a booking
SELECT * FROM Rooms
WHERE RoomID = 101
  AND AvailabilityStatus = 'Available'
  AND RoomID NOT IN (
    SELECT RoomID FROM Bookings
    WHERE (CheckInDate BETWEEN '2024-12-15' AND '2024-12-18')
      OR (CheckOutDate BETWEEN '2024-12-15' AND '2024-12-18')
  );
-- If no rows are returned, the room is not available
```

#### **2. Handling Multiple Bookings for the Same Guest**

When a guest books a room multiple times, we need to ensure that their booking history is updated properly.

```sql
-- Insert a new booking and update the guest’s booking history (if needed)
INSERT INTO Bookings (GuestID, RoomID, CheckInDate, CheckOutDate, PaymentStatus, SpecialRequests, BookingStatus)
VALUES (1, 101, '2024-12-15 14:00:00', '2024-12-18 11:00:00', 'Pending', 'Non-smoking', 'Confirmed');

-- Optionally, you can store guest booking history in a separate log or column.
-- For instance, you can append new booking data to a booking history field, or store it in a separate table.
UPDATE Guests
SET BookingHistory = CONCAT(BookingHistory, ', BookingID: ', LAST_INSERT_ID())
WHERE GuestID = 1;
```

#### **3. Service Availability (Preventing Overbooking of Services)**

To handle service availability, we must ensure that services like "Spa" or "Tour" do not exceed capacity. Assuming there's a capacity field for each service type:

```sql
-- Check availability for a service before adding it to a booking
SELECT * FROM Services
WHERE ServiceType = 'Spa'
  AND ServiceDate = '2024-12-16 10:00:00'
  AND (SELECT COUNT(*) FROM Services WHERE ServiceType = 'Spa' AND ServiceDate = '2024-12-16 10:00:00') < 5; -- Assume max 5 services can be booked at this time
-- If no rows are returned, the service can be booked
```

#### **4. Handling Cancellations**

When a booking is canceled, the room should be marked as available, and any associated services should also be canceled. Here's how to handle cancellations:

```sql
-- Mark the room as available when the booking is canceled
UPDATE Rooms
SET AvailabilityStatus = 'Available'
WHERE RoomID IN (SELECT RoomID FROM Bookings WHERE BookingID = 101);

-- Mark services as canceled when the booking is canceled
UPDATE Services
SET ServiceStatus = 'Canceled'
WHERE BookingID = 101;

-- Update the booking status
UPDATE Bookings
SET BookingStatus = 'Canceled'
WHERE BookingID = 101;
```

#### **5. Role-Based Access (Handling Staff Permissions)**

To ensure that staff have different access levels based on their roles, you can query the staff table to filter access according to the role. For example:

```sql
-- Example: Only managers or admins can view certain reports
SELECT * FROM Reports
WHERE ReportType = 'Revenue'
  AND EXISTS (SELECT 1 FROM Staff WHERE StaffID = 1 AND Role = 'Manager' AND RoleBasedAccess = 'Admin');
-- If the staff member has the correct role, the report will be retrieved
```

---

### 3. **Reporting Queries**

#### **Occupancy Report**

To generate an occupancy report, you would typically query the `Bookings` and `Rooms` tables to calculate the occupancy rate for each room or for the entire hotel.

```sql
-- Example: Generate an occupancy report for a specific date range
SELECT r.RoomType, COUNT(b.BookingID) AS BookedRooms, COUNT(r.RoomID) AS TotalRooms,
       (COUNT(b.BookingID) / COUNT(r.RoomID)) * 100 AS OccupancyRate
FROM Rooms r
LEFT JOIN Bookings b ON r.RoomID = b.RoomID
WHERE b.CheckInDate BETWEEN '2024-12-01' AND '2024-12-31'
GROUP BY r.RoomType;
```

#### **Revenue Report**

To generate a revenue report based on bookings, you can sum the `PricePerNight` of rooms booked during a given period.

```sql
-- Example: Generate a revenue report for a specific date range
SELECT SUM(r.PricePerNight * DATEDIFF(b.CheckOutDate, b.CheckInDate)) AS TotalRevenue
FROM Rooms r
JOIN Bookings b ON r.RoomID = b.RoomID
WHERE b.CheckInDate BETWEEN '2024-12-01' AND '2024-12-31'
  AND b.BookingStatus = 'Completed';
```

---

### Final Notes:

- Ensure that **foreign key constraints** are properly defined to maintain data integrity between tables.
- **Triggers or Stored Procedures** can be used to automate tasks like updating availability, generating reports, or handling cancellations and overbookings.
- **Indexes** should be created on frequently queried fields (e.g., `BookingID`, `GuestID`, `RoomID`, etc.) to optimize query performance.

---

## OOP Representation:

---

## 1. Data Models

### 1.1 Guest

Stores essential guest information and preferences.  
For full booking history, either store it here as a list or retrieve it via a `Booking` repository.

```csharp
public class Guest
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string ContactInfo { get; set; }  // e.g., phone/email
    public string Preferences { get; set; }   // e.g., "Non-smoking room, extra pillows"

    public Guest(int id, string name, string contactInfo, string preferences)
    {
        Id = id;
        Name = name;
        ContactInfo = contactInfo;
        Preferences = preferences;
    }

    public override string ToString()
    {
        return $"{Name} (ID: {Id}), Contact: {ContactInfo}, Prefs: {Preferences}";
    }
}
```

### 1.2 Room

Represents a hotel room with details about its type, pricing, and availability.

```csharp
public class Room
{
    public int Id { get; set; }
    public string RoomType { get; set; }     // e.g., "Single", "Double", "Suite"
    public decimal PricePerNight { get; set; }
    public int FloorNumber { get; set; }
    public bool IsAvailable { get; set; }

    public Room(int id, string roomType, decimal pricePerNight, int floorNumber)
    {
        Id = id;
        RoomType = roomType;
        PricePerNight = pricePerNight;
        FloorNumber = floorNumber;
        IsAvailable = true; // default to available
    }

    public override string ToString()
    {
        return $"Room #{Id}, {RoomType}, Floor {FloorNumber}, Price: {PricePerNight:C}, Available: {IsAvailable}";
    }
}
```

### 1.3 Booking

A `Booking` ties a `Guest` to a `Room`, with details about the stay (check-in, check-out, payment status, etc.).

```csharp
public class Booking
{
    public int Id { get; set; }
    public Guest Guest { get; set; }
    public Room Room { get; set; }
    public DateTime CheckInDate { get; set; }
    public DateTime CheckOutDate { get; set; }
    public string PaymentStatus { get; set; }  // e.g., "Paid", "Pending"
    public string BookingStatus { get; set; }  // e.g., "Confirmed", "Cancelled", "Completed"
    public string SpecialRequests { get; set; }

    public Booking(int id, Guest guest, Room room, DateTime checkIn, DateTime checkOut)
    {
        Id = id;
        Guest = guest;
        Room = room;
        CheckInDate = checkIn;
        CheckOutDate = checkOut;
        PaymentStatus = "Pending";
        BookingStatus = "Confirmed";
        SpecialRequests = "";
    }

    public int TotalNights => (CheckOutDate - CheckInDate).Days;

    public decimal CalculateCost()
    {
        // Basic cost calculation: nights * price per night
        return TotalNights * Room.PricePerNight;
    }

    public override string ToString()
    {
        return $"Booking #{Id}, Guest: {Guest.Name}, Room #{Room.Id}, {CheckInDate.ToShortDateString()} - {CheckOutDate.ToShortDateString()}, Status: {BookingStatus}";
    }
}
```

### 1.4 Service

Represents an additional service used by a guest during their stay (e.g., room service, spa, tours), linked to a specific `Booking`.

```csharp
public class Service
{
    public int Id { get; set; }
    public string ServiceType { get; set; }  // e.g., "Room Service", "Spa", "Tour Booking"
    public decimal Cost { get; set; }
    public DateTime DateUsed { get; set; }
    public Booking LinkedBooking { get; set; }

    public string ServiceStatus { get; set; } // e.g., "Requested", "Completed", "Cancelled"

    public Service(int id, string serviceType, decimal cost, DateTime dateUsed, Booking booking)
    {
        Id = id;
        ServiceType = serviceType;
        Cost = cost;
        DateUsed = dateUsed;
        LinkedBooking = booking;
        ServiceStatus = "Requested";
    }

    public override string ToString()
    {
        return $"Service #{Id}, {ServiceType}, Cost: {Cost:C}, Date: {DateUsed.ToShortDateString()}, Booking #{LinkedBooking.Id}, Status: {ServiceStatus}";
    }
}
```

### 1.5 Staff

Represents hotel staff members, with role-based information.

```csharp
public class Staff
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Role { get; set; }         // e.g., "Receptionist", "Housekeeping", "Manager"
    public string Schedule { get; set; }     // e.g., "Mon-Fri 9AM-5PM"

    // You could track staff performance or tasks completed here.

    public Staff(int id, string name, string role, string schedule)
    {
        Id = id;
        Name = name;
        Role = role;
        Schedule = schedule;
    }

    public override string ToString()
    {
        return $"{Name} (ID: {Id}, {Role}), Schedule: {Schedule}";
    }
}
```

---

## 2. Repositories (In-Memory)

We’ll define a generic `IRepository<T>` interface for CRUD operations, then create an **in-memory** `GenericRepository<T>` for each entity. In a production system, you’d likely replace these with database-backed repositories.

```csharp
public interface IRepository<T>
{
    void Add(T entity);
    T GetById(int id);
    IEnumerable<T> GetAll();
    void Update(T entity);
    void Delete(int id);
}
```

### 2.1 GenericRepository

```csharp
public class GenericRepository<T> : IRepository<T>
{
    private readonly List<T> _items = new List<T>();

    public void Add(T entity) => _items.Add(entity);

    public T GetById(int id)
    {
        // Uses reflection to find a property "Id" of type int.
        // For a production scenario, consider a more robust approach.
        return _items.FirstOrDefault(x =>
            (int)x.GetType().GetProperty("Id").GetValue(x) == id
        );
    }

    public IEnumerable<T> GetAll() => _items;

    public void Update(T entity)
    {
        var idValue = (int)entity.GetType().GetProperty("Id").GetValue(entity);
        var existing = GetById(idValue);
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

_(We can then instantiate `GenericRepository<Guest>`, `GenericRepository<Room>`, etc.)_

---

## 3. Core Service: `HotelService`

The `HotelService` class orchestrates main functionalities like:

- Creating/canceling/updating bookings
- Checking room availability
- Linking services to bookings
- Generating basic reports (room occupancy, revenue by service, guest preferences)

```csharp
public class HotelService
{
    private readonly IRepository<Guest> _guestRepo;
    private readonly IRepository<Room> _roomRepo;
    private readonly IRepository<Booking> _bookingRepo;
    private readonly IRepository<Service> _serviceRepo;
    private readonly IRepository<Staff> _staffRepo;

    public HotelService(
        IRepository<Guest> guestRepo,
        IRepository<Room> roomRepo,
        IRepository<Booking> bookingRepo,
        IRepository<Service> serviceRepo,
        IRepository<Staff> staffRepo)
    {
        _guestRepo = guestRepo;
        _roomRepo = roomRepo;
        _bookingRepo = bookingRepo;
        _serviceRepo = serviceRepo;
        _staffRepo = staffRepo;
    }

    // ------------------------------
    // Booking Management
    // ------------------------------

    /// <summary>
    /// Creates a booking for a guest with a specified room and date range.
    /// Checks room availability before confirming.
    /// </summary>
    public Booking CreateBooking(int guestId, int roomId, DateTime checkIn, DateTime checkOut, string specialRequests)
    {
        var guest = _guestRepo.GetById(guestId);
        if (guest == null) throw new Exception("Guest not found.");

        var room = _roomRepo.GetById(roomId);
        if (room == null) throw new Exception("Room not found.");
        if (!room.IsAvailable)
            throw new Exception($"Room #{room.Id} is not currently available.");

        if (checkIn >= checkOut)
            throw new Exception("Check-in date must be before check-out date.");

        // Mark room as unavailable for the duration
        room.IsAvailable = false;
        _roomRepo.Update(room);

        var newBooking = new Booking(GenerateBookingId(), guest, room, checkIn, checkOut)
        {
            SpecialRequests = specialRequests
        };

        _bookingRepo.Add(newBooking);
        Console.WriteLine($"Created {newBooking}");
        return newBooking;
    }

    /// <summary>
    /// Completes or cancels a booking, updating room availability.
    /// </summary>
    public void UpdateBookingStatus(int bookingId, string newStatus)
    {
        var booking = _bookingRepo.GetById(bookingId);
        if (booking == null) throw new Exception("Booking not found.");

        booking.BookingStatus = newStatus;
        _bookingRepo.Update(booking);

        // If booking is completed or cancelled, free up the room
        if (newStatus == "Completed" || newStatus == "Cancelled")
        {
            var room = booking.Room;
            if (room != null)
            {
                room.IsAvailable = true;
                _roomRepo.Update(room);
            }
        }

        Console.WriteLine($"Booking #{bookingId} status updated to {newStatus}.");
    }

    /// <summary>
    /// Updates the payment status of a booking (e.g., to "Paid").
    /// </summary>
    public void UpdatePaymentStatus(int bookingId, string paymentStatus)
    {
        var booking = _bookingRepo.GetById(bookingId);
        if (booking == null) throw new Exception("Booking not found.");

        booking.PaymentStatus = paymentStatus;
        _bookingRepo.Update(booking);

        Console.WriteLine($"Booking #{bookingId} payment status updated to {paymentStatus}.");
    }

    // ------------------------------
    // Service Management
    // ------------------------------

    /// <summary>
    /// Adds a service request (room service, spa, etc.) to an existing booking.
    /// </summary>
    public Service RequestService(int bookingId, string serviceType, decimal cost)
    {
        var booking = _bookingRepo.GetById(bookingId);
        if (booking == null) throw new Exception("Booking not found.");

        var service = new Service(GenerateServiceId(), serviceType, cost, DateTime.Now, booking);
        _serviceRepo.Add(service);

        Console.WriteLine($"Service requested: {service}");
        return service;
    }

    public void UpdateServiceStatus(int serviceId, string newStatus)
    {
        var service = _serviceRepo.GetById(serviceId);
        if (service == null) throw new Exception("Service not found.");

        service.ServiceStatus = newStatus;
        _serviceRepo.Update(service);

        Console.WriteLine($"Service #{serviceId} status updated to {newStatus}.");
    }

    // ------------------------------
    // Reporting
    // ------------------------------

    /// <summary>
    /// Room Occupancy Report: which rooms are occupied and which are free.
    /// </summary>
    public IEnumerable<Room> GetOccupiedRooms()
    {
        return _roomRepo.GetAll().Where(r => !r.IsAvailable);
    }

    /// <summary>
    /// Revenue by Service: sums cost of each type of service for all bookings.
    /// Returns a dictionary or a list of (ServiceType, TotalRevenue).
    /// </summary>
    public List<(string serviceType, decimal totalRevenue)> GetRevenueByService()
    {
        var grouped = _serviceRepo
            .GetAll()
            .GroupBy(s => s.ServiceType)
            .Select(g => (serviceType: g.Key, totalRevenue: g.Sum(s => s.Cost)))
            .ToList();

        return grouped;
    }

    /// <summary>
    /// Guest Preferences Report: optionally, you can list top preferences or
    /// see how many guests requested certain things, etc.
    /// For demonstration, we just list all guest preferences.
    /// </summary>
    public IEnumerable<string> GetGuestPreferences()
    {
        return _guestRepo.GetAll().Select(g => g.Preferences).Distinct();
    }

    // ------------------------------
    // Helper ID Generators
    // ------------------------------

    private int GenerateBookingId()
    {
        return new Random().Next(1000, 9999);
    }

    private int GenerateServiceId()
    {
        return new Random().Next(10000, 99999);
    }
}
```

---

## 4. Demonstration / Usage

Below is a `Program` class that seeds some data and demonstrates how to create bookings, request services, and generate reports.

```csharp
public class Program
{
    public static void Main()
    {
        // Create in-memory repositories
        var guestRepo = new GenericRepository<Guest>();
        var roomRepo = new GenericRepository<Room>();
        var bookingRepo = new GenericRepository<Booking>();
        var serviceRepo = new GenericRepository<Service>();
        var staffRepo = new GenericRepository<Staff>();

        // Create the HotelService
        var hotelService = new HotelService(guestRepo, roomRepo, bookingRepo, serviceRepo, staffRepo);

        // 1) Seed Data
        SeedData(guestRepo, roomRepo, staffRepo);

        // 2) Create a Booking
        var booking = hotelService.CreateBooking(
            guestId: 1,
            roomId: 101,
            checkIn: DateTime.Today,
            checkOut: DateTime.Today.AddDays(3),
            specialRequests: "Extra pillows, late check-in"
        );

        // 3) Update Payment Status
        hotelService.UpdatePaymentStatus(booking.Id, "Paid");

        // 4) Request Additional Service (e.g., Room Service)
        var service1 = hotelService.RequestService(booking.Id, "Room Service - Lunch", 29.99m);

        // 5) Update Service Status
        hotelService.UpdateServiceStatus(service1.Id, "Completed");

        // 6) Generate some reports

        // a) Room Occupancy
        Console.WriteLine("\n--- Room Occupancy Report ---");
        var occupiedRooms = hotelService.GetOccupiedRooms();
        if (occupiedRooms.Any())
        {
            foreach (var room in occupiedRooms) Console.WriteLine(room);
        }
        else
        {
            Console.WriteLine("No rooms are currently occupied.");
        }

        // b) Revenue by Service
        Console.WriteLine("\n--- Revenue by Service ---");
        var serviceRevenues = hotelService.GetRevenueByService();
        foreach (var (type, revenue) in serviceRevenues)
        {
            Console.WriteLine($"{type}: {revenue:C}");
        }

        // c) Guest Preferences
        Console.WriteLine("\n--- Guest Preferences Report ---");
        var preferences = hotelService.GetGuestPreferences();
        foreach (var pref in preferences)
        {
            Console.WriteLine($"Preference: {pref}");
        }

        // 7) Complete the booking
        hotelService.UpdateBookingStatus(booking.Id, "Completed");
    }

    private static void SeedData(
        IRepository<Guest> guestRepo,
        IRepository<Room> roomRepo,
        IRepository<Staff> staffRepo)
    {
        // Guests
        var guest1 = new Guest(1, "Alice Johnson", "alice@example.com", "Non-smoking room, near elevator");
        var guest2 = new Guest(2, "Bob Smith", "bob@example.com", "Sea view if possible, allergic to feathers");
        guestRepo.Add(guest1);
        guestRepo.Add(guest2);

        // Rooms
        var room1 = new Room(101, "Single", 99.99m, 1);
        var room2 = new Room(102, "Double", 149.99m, 2);
        var room3 = new Room(201, "Suite", 299.99m, 2);
        roomRepo.Add(room1);
        roomRepo.Add(room2);
        roomRepo.Add(room3);

        // Staff
        var staff1 = new Staff(1001, "John Reception", "Receptionist", "8AM-4PM");
        var staff2 = new Staff(1002, "Mary Housekeeping", "Housekeeping", "6AM-2PM");
        staffRepo.Add(staff1);
        staffRepo.Add(staff2);

        // By default, rooms are available. No bookings yet.
    }
}
```

### Explanation of the Flow

1. **Seeding**: We add a couple of guests, some rooms, and staff members.
2. **Create Booking**: Guest #1 books Room #101 for 3 nights. The system checks availability, marks the room as no longer available, and creates a `Booking`.
3. **Update Payment Status**: We set the booking’s payment status to “Paid.”
4. **Request Additional Service**: The guest requests a lunch via room service. We create a `Service` record linked to that booking.
5. **Update Service**: We mark that service as completed once delivered.
6. **Generate Reports**:
   - **Room Occupancy**: We see which rooms are currently occupied.
   - **Revenue by Service**: Summarize total revenue for each service type.
   - **Guest Preferences**: Show all preferences from guests.
7. **Complete the Booking**: We update the booking status to “Completed,” which frees up the room.

---

## Final Thoughts

- **Domain Classes**: `Guest`, `Room`, `Booking`, `Service`, and `Staff` represent the main entities.
- **Repositories**: We use a generic in-memory approach to store these entities.
- **Service Layer** (`HotelService`): Orchestrates business logic (creating bookings, managing room availability, linking services, generating basic reports).
- **Scalability**: This design easily extends to more complex features (e.g., loyalty programs, advanced scheduling, multi-property management).
- **Security & Role-Based Access**: In a real system, staff roles (e.g., “Receptionist,” “Manager,” “Housekeeping”) could be leveraged to limit certain operations in the `HotelService` or user interface layer.
- **Reports**: We demonstrated basic occupancy and revenue-by-service reports. Additional or more sophisticated reports can be added similarly.

---
