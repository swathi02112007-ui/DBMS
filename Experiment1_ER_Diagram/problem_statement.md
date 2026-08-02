# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="955" height="674" alt="Screenshot 2026-08-02 174656" src="https://github.com/user-attachments/assets/90f360e0-36f2-4312-8851-b7b28937f1f0" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|----------------------|-------|
| MEMBER | MembershipNo (PK), Name (Composite: FirstName, LastName), DOB, Phone (Multivalued), Email (AK), Age (Derived), MembershipType, StartDate | Stores member details and membership information. |
| PROGRAM | ProgramCode (PK), ProgramName, Duration, Fee | Stores details of fitness programs offered by the gym. |
| TRAINER | EmployeeNo (PK), Name (Composite), Specialization, Qualification (Multivalued), Experience (Derived) | Stores trainer information and qualifications. |
| ENROLLMENT | RegistrationNo (PK), MembershipNo (FK), ProgramCode (FK), JoinDate | Records member enrollment in fitness programs. |
| PERSONAL_SESSION | AppointmentNo (PK), MembershipNo (FK), EmployeeNo (FK), SessionDate, Duration | Stores personal training session bookings. |
| ATTENDANCE | RecordNo (PK), AppointmentNo (FK), Status | Records attendance for each personal training session. |
| PAYMENT | ReceiptNo (PK), MembershipNo (FK), AppointmentNo (FK), Amount, PaymentDate, PaymentMode | Tracks payments for memberships and training sessions. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|-------------|-------------|---------------|-------|
| MEMBER — ENROLLMENT | 1 : M | Partial | A member may enroll in multiple programs. |
| PROGRAM — ENROLLMENT | 1 : M | Total | Every enrollment must belong to one program. |
| PROGRAM — TRAINER | M : N | Partial | A program can have multiple trainers, and a trainer can teach multiple programs. |
| MEMBER — PERSONAL_SESSION | 1 : M | Partial | A member may book multiple personal training sessions. |
| TRAINER — PERSONAL_SESSION | 1 : M | Partial | A trainer may conduct multiple personal training sessions. |
| PERSONAL_SESSION — ATTENDANCE | 1 : 1 | Total | Each personal session has one attendance record. |
| MEMBER — PAYMENT | 1 : M | Partial | A member can make multiple payments. |
| PERSONAL_SESSION — PAYMENT | 1 : M | Partial | A personal session may be associated with one or more payment records. |

### Assumptions

- A member can enroll in multiple fitness programs.
- Each enrollment belongs to one member and one program.
- A program can be assigned to multiple trainers, and a trainer can teach multiple programs.
- Personal training sessions are booked by one member with one trainer.
- Attendance is recorded only for personal training sessions.
- Each personal training session has one attendance record.
- Payments may be made for memberships or personal training sessions.
- Each payment is made by one member and is linked to at most one personal training session.
# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="926" height="662" alt="Screenshot 2026-08-02 174623" src="https://github.com/user-attachments/assets/e6c889b4-28a6-4a9c-b4e2-9641d9045453" />

### Entities and Attributes
| Entity | Attributes (PK, FK) | Notes |
|--------|----------------------|-------|
| MEMBER | MemberID (PK), Name (Composite: FirstName, LastName), Phone, Email (AK), MembershipDate | Stores registered library member details. |
| BOOK | BookID (PK), ISBN (AK), Title, Author, Category, Publisher | Stores information about library books. |
| LOAN | LoanID (PK), LoanDate, DueDate, ReturnDate, MemberID (FK), BookID (FK) | Tracks book borrowing and return transactions. |
| FINE | FineID (PK), Amount, PaidStatus, LoanID (FK) | Stores overdue fine details for loans. |
| EVENT | EventID (PK), EventName, EventDate, EventType | Stores cultural and library event information. |
| EVENT_REGISTRATION | RegistrationID (PK), MemberID (FK), EventID (FK), RegistrationDate | Records member registrations for events. |
| SPEAKER | SpeakerID (PK), Name, Expertise, Contact | Stores event speaker or author details. |
| EVENT_SPEAKER | EventID (FK), SpeakerID (FK) | Associative entity linking events and speakers. |
| ROOM | RoomID (PK), RoomName, Capacity, Location | Stores library room information. |
| ROOM_BOOKING | BookingID (PK), BookingDate, Purpose, RoomID (FK), EventID (FK) | Records room bookings for events and study purposes. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|-------------|-------------|---------------|-------|
| MEMBER — LOAN | 1 : M | Total for LOAN | A member can borrow many books. |
| BOOK — LOAN | 1 : M | Total for LOAN | A book can be borrowed multiple times over time. |
| LOAN — FINE | 1 : 0..1 | Partial for FINE | A loan may or may not have a fine. |
| MEMBER — EVENT_REGISTRATION | 1 : M | Partial | A member may register for multiple events. |
| EVENT — EVENT_REGISTRATION | 1 : M | Total for EVENT_REGISTRATION | Each registration belongs to one event. |
| EVENT — SPEAKER | M : N | Total for EVENT | An event can have one or more speakers, and a speaker can participate in multiple events. |
| ROOM — ROOM_BOOKING | 1 : M | Total for ROOM_BOOKING | A room can be booked multiple times. |
| EVENT — ROOM_BOOKING | 1 : M | Partial | An event may require one or more room bookings. |

### Assumptions

- A member can borrow multiple books at different times.
- A book can be borrowed by only one member at a time.
- Each loan is associated with one member and one book.
- A fine is generated only for overdue loans.
- Members may register for multiple events.
- Each event has at least one speaker.
- A speaker may participate in multiple events.
- Rooms can be booked for events or study purposes.
- Each room booking is associated with one room and one event.
  
---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="909" height="694" alt="Screenshot 2026-08-02 192050" src="https://github.com/user-attachments/assets/6ee78457-6c4b-493b-bf84-4bf5bca33aae" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|----------------------|-------|
| CUSTOMER | CustomerID (PK), Name (Composite: FirstName, LastName), Phone (Multivalued), Email (AK), LoyaltyPoints, Age (Derived) | Stores customer details and loyalty information. |
| TABLE | TableID (PK), TableNumber (AK), Capacity, Location, Status | Stores restaurant table information and availability status. |
| RESERVATION | ReservationID (PK), ReservationDate, ReservationTime, NumberOfGuests, ReservationType (Reserved/Walk-in), CustomerID (FK), TableID (FK), WaiterID (FK) | Records table reservations and walk-in dining details. |
| WAITER | WaiterID (PK), Name, Phone, Shift, ExperienceYears (Derived) | Stores waiter details and work shift information. |
| ORDER | OrderID (PK), OrderTime, OrderStatus, ReservationID (FK) | Stores food orders placed for a reservation. |
| ORDER_ITEM | OrderID (PK, FK), DishID (PK, FK), Quantity, ItemPrice | Stores dishes included in each order. |
| DISH | DishID (PK), DishName, Price, AvailabilityStatus, CategoryID (FK) | Stores menu item details and availability. |
| CATEGORY | CategoryID (PK), CategoryName | Stores dish categories such as Starter, Main Course, and Dessert. |
| BILL | BillID (PK), ReservationID (FK), FoodAmount, ServiceCharge, Tax, TotalAmount (Derived), PaymentMethod, PaymentStatus | Stores billing and payment information for each reservation. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|-------------|-------------|---------------|-------|
| CUSTOMER — RESERVATION | 1 : M | Reservation – Total | A customer can make multiple reservations; each reservation belongs to one customer. |
| TABLE — RESERVATION | 1 : M | Reservation – Total | Each reservation is assigned one table; a table can be assigned to many reservations over time. |
| WAITER — RESERVATION | 1 : M | Reservation – Total | One waiter can serve multiple reservations. |
| RESERVATION — ORDER | 1 : M | Order – Total | A reservation can generate multiple food orders. |
| ORDER — ORDER_ITEM | 1 : M | Order_Item – Total | Each order contains one or more order items. |
| DISH — ORDER_ITEM | 1 : M | Order_Item – Total | A dish can appear in many order items. |
| CATEGORY — DISH | 1 : M | Dish – Total | Each dish belongs to one category. |
| RESERVATION — BILL | 1 : 1 | Bill – Total | Each reservation generates exactly one bill. |

### Assumptions

- A customer can make multiple reservations.
- Walk-in customers are also recorded as reservations.
- Each reservation is assigned one table and one waiter.
- A table can be reserved multiple times at different times.
- Each order belongs to one reservation.
- An order can contain multiple dishes through ORDER_ITEM.
- Every dish belongs to one category.
- Each reservation generates exactly one bill.
- The total bill amount is calculated from food amount, service charge, and tax.
- Payment is recorded only after the bill is generated.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
