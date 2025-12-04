# SajiloYatra Database System
## CC5051 Databases Coursework - Autumn Semester 2025

---

## Part 1: Introduction (15%)

### 1.1 Business Introduction and Forte (5 marks)

**SajiloYatra** is an innovative intercity travel service company founded by Mr. Kiran Thapa in Pokhara, Nepal. The name "SajiloYatra" translates to "Easy Journey" in Nepali, reflecting the company's core mission to provide seamless, reliable, and efficient transportation services across major cities of Nepal including Kathmandu, Pokhara, Chitwan, and Butwal.

**Business Forte:**
SajiloYatra's competitive advantage lies in its modernized approach to intercity travel management through:
- **Digital Transformation**: Implementation of an online booking and management system that eliminates traditional inefficiencies
- **Centralized Operations**: Unified platform for managing buses, routes, passengers, and staff
- **Customer-Centric Service**: Multiple booking classes (Regular, Premium, VIP) catering to diverse passenger needs
- **Operational Excellence**: Real-time tracking of trips, payments, and vehicle availability
- **Staff Management**: Systematic assignment and tracking of drivers and conductors

The company addresses critical pain points in Nepal's intercity travel sector including overbooking, poor coordination, and lack of transparency in scheduling and payments.

### 1.2 Current Business Activities and Operations (5 marks)

**Core Operations:**

1. **Route Management**: SajiloYatra operates across multiple predefined routes connecting major cities. Each route has specific origin and destination points with associated distances and estimated travel durations.

2. **Trip Scheduling**: The company schedules multiple trips daily along each route. Trips include specific departure and arrival times, and are assigned to available buses based on operational capacity.

3. **Fleet Management**: The company maintains a fleet of buses with varying capacities. Buses are assigned to specific routes and may be temporarily unavailable due to maintenance or operational constraints.

4. **Staff Operations**: The company employs drivers and conductors who are assigned to buses for trip operations. Staff members are responsible for passenger safety, boarding assistance, and compliance with regulations.

5. **Booking System**: Passengers can book trips through the system, selecting from different booking classes. Each booking is recorded with booking date, class type, and status tracking.

6. **Ticketing Process**: Upon booking confirmation, tickets are generated containing unique ticket IDs, fare details, and issue dates. Tickets serve as proof of reservation for specific trips.

7. **Payment Processing**: The system handles payment transactions with multiple payment methods. Payment records are linked to tickets and include payment amount, date, and transaction status.

8. **Passenger Management**: The system maintains comprehensive passenger records including contact information and booking history. Passengers can book multiple trips, and their preferences such as luggage requirements are tracked.

### 1.3 Business Rules (5 marks)

The following business rules govern the SajiloYatra database system structure:

**BR1: Route Rules**
- Each route must have a unique route identifier
- A route connects exactly two locations (origin and destination)
- Multiple trips can be scheduled on a single route
- Each route must have at least one bus assigned to it

**BR2: Trip Rules**
- Each trip must be associated with exactly one route
- A trip must have a unique trip identifier
- Trips must record departure time, arrival time, and trip date
- Multiple passengers can travel on a single trip
- A trip operates on exactly one bus

**BR3: Bus Rules**
- Each bus must have a unique bus identifier and registration number
- A bus has a defined seating capacity
- A bus can be assigned to multiple trips over time
- Buses may have availability status (Available, Maintenance, Unavailable)

**BR4: Staff Rules**
- Each staff member must have a unique staff identifier
- Staff can be categorized by role (Driver, Conductor)
- Multiple staff members are assigned to each bus for operations
- Staff information includes name, contact details, and role

**BR5: Passenger Rules**
- Each passenger must have a unique passenger identifier
- Passengers must provide contact information (phone, email)
- A passenger can make multiple bookings over time
- Passenger information is recorded once and referenced in multiple bookings

**BR6: Booking Rules**
- Each booking links a passenger to a specific trip
- Bookings must specify class type (Regular, Premium, VIP)
- Each booking has a booking date and status (Confirmed, Cancelled, Pending)
- A booking generates exactly one ticket upon confirmation

**BR7: Ticket Rules**
- Each ticket must have a unique ticket identifier
- A ticket is associated with exactly one booking
- Tickets record fare amount and issue date
- A ticket may exist before payment is completed

**BR8: Payment Rules**
- Each payment must have a unique payment identifier
- A payment is linked to exactly one ticket
- Payments record amount, payment date, and payment method
- Payment status indicates whether a ticket is paid or unpaid
- Payment amount must match the ticket fare

**BR9: Referential Integrity Rules**
- Deletion of a route should cascade to trips on that route
- Deletion of a trip should cascade to bookings for that trip
- Passenger and staff records should be retained for historical data
- Payment records must reference existing tickets

**BR10: Constraint Rules**
- Trip departure time must be before arrival time
- Booking date must be before or on trip departure date
- Payment date cannot be before ticket issue date
- Bus capacity must be a positive integer
- Fare amounts must be positive values

---

## Part 2: Initial ERD (5%)

### 2.1 Identification of Entities and Attributes (3 marks)

**Entity 1: PASSENGER**
- **Passenger_ID** (Primary Key)
- Passenger_Name
- Phone_Number
- Email_Address
- Address

**Entity 2: ROUTE**
- **Route_ID** (Primary Key)
- Origin
- Destination
- Distance_KM
- Estimated_Duration

**Entity 3: BUS**
- **Bus_ID** (Primary Key)
- Bus_Registration_Number
- Capacity
- Bus_Type
- Availability_Status

**Entity 4: TRIP**
- **Trip_ID** (Primary Key)
- Route_ID (Foreign Key)
- Bus_ID (Foreign Key)
- Trip_Date
- Departure_Time
- Arrival_Time

**Entity 5: STAFF**
- **Staff_ID** (Primary Key)
- Staff_Name
- Role
- Phone_Number
- Hire_Date

**Entity 6: BOOKING**
- **Booking_ID** (Primary Key)
- Passenger_ID (Foreign Key)
- Trip_ID (Foreign Key)
- Booking_Date
- Booking_Class
- Booking_Status

**Entity 7: TICKET**
- **Ticket_ID** (Primary Key)
- Booking_ID (Foreign Key)
- Fare_Amount
- Issue_Date

**Entity 8: PAYMENT**
- **Payment_ID** (Primary Key)
- Ticket_ID (Foreign Key)
- Payment_Amount
- Payment_Date
- Payment_Method

**Entity 9: BUS_STAFF_ASSIGNMENT**
- **Assignment_ID** (Primary Key)
- Bus_ID (Foreign Key)
- Staff_ID (Foreign Key)
- Assignment_Date

### 2.2 Initial Entity Relationship Diagram (2 marks)

```
Initial ERD Structure (Before Normalization):

PASSENGER (Passenger_ID, Passenger_Name, Phone_Number, Email_Address, Address)
    |
    | 1:M (One passenger can make many bookings)
    |
BOOKING (Booking_ID, Passenger_ID, Trip_ID, Booking_Date, Booking_Class, Booking_Status)
    |
    | 1:1 (One booking generates one ticket)
    |
TICKET (Ticket_ID, Booking_ID, Fare_Amount, Issue_Date)
    |
    | 1:1 (One ticket has one payment)
    |
PAYMENT (Payment_ID, Ticket_ID, Payment_Amount, Payment_Date, Payment_Method)

ROUTE (Route_ID, Origin, Destination, Distance_KM, Estimated_Duration)
    |
    | 1:M (One route has many trips)
    |
TRIP (Trip_ID, Route_ID, Bus_ID, Trip_Date, Departure_Time, Arrival_Time)
    |
    | M:1 (Many trips use one bus)
    |
BUS (Bus_ID, Bus_Registration_Number, Capacity, Bus_Type, Availability_Status)
    |
    | M:N (Many buses have many staff through assignment)
    |
STAFF (Staff_ID, Staff_Name, Role, Phone_Number, Hire_Date)

BUS_STAFF_ASSIGNMENT (Assignment_ID, Bus_ID, Staff_ID, Assignment_Date)
```

**Relationships:**
1. PASSENGER → BOOKING (1:M) - One passenger makes many bookings
2. TRIP → BOOKING (1:M) - One trip has many bookings
3. BOOKING → TICKET (1:1) - One booking generates one ticket
4. TICKET → PAYMENT (1:1) - One ticket has one payment
5. ROUTE → TRIP (1:M) - One route has many trips
6. BUS → TRIP (1:M) - One bus operates many trips
7. BUS ↔ STAFF (M:N) - Many-to-many through BUS_STAFF_ASSIGNMENT

---

## Part 3: Normalization (20%)

### Unnormalized Form (UNF)

**Initial Unnormalized Data Structure:**

```
SAJILOYATRA_SYSTEM (
    Passenger_ID, Passenger_Name, Phone_Number, Email_Address, Address,
    {Booking_ID, Booking_Date, Booking_Class, Booking_Status,
        Trip_ID, Trip_Date, Departure_Time, Arrival_Time,
            Route_ID, Origin, Destination, Distance_KM, Estimated_Duration,
            Bus_ID, Bus_Registration_Number, Capacity, Bus_Type, Availability_Status,
            {Staff_ID, Staff_Name, Role, Staff_Phone, Hire_Date},
        Ticket_ID, Fare_Amount, Issue_Date,
            Payment_ID, Payment_Amount, Payment_Date, Payment_Method
    }
)
```

**Problems in UNF:**
- Repeating groups (multiple bookings per passenger)
- Nested repeating groups (multiple staff per bus)
- Data redundancy
- Update anomalies

### First Normal Form (1NF)

**Objective:** Remove repeating groups and ensure atomic values.

**Step 1: Flatten the structure by removing nested groups**

After removing repeating groups, we separate into multiple relations:

**PASSENGER_BOOKING_1NF**
```
(Passenger_ID, Passenger_Name, Phone_Number, Email_Address, Address,
 Booking_ID, Booking_Date, Booking_Class, Booking_Status,
 Trip_ID, Trip_Date, Departure_Time, Arrival_Time,
 Route_ID, Origin, Destination, Distance_KM, Estimated_Duration,
 Bus_ID, Bus_Registration_Number, Capacity, Bus_Type, Availability_Status,
 Ticket_ID, Fare_Amount, Issue_Date,
 Payment_ID, Payment_Amount, Payment_Date, Payment_Method)
```
**Primary Key:** Booking_ID

**BUS_STAFF_1NF**
```
(Bus_ID, Bus_Registration_Number, Capacity, Bus_Type, Availability_Status,
 Staff_ID, Staff_Name, Role, Staff_Phone, Hire_Date, Assignment_Date)
```
**Primary Key:** (Bus_ID, Staff_ID)

**Functional Dependencies in 1NF:**

For PASSENGER_BOOKING_1NF:
- Booking_ID → Passenger_ID, Booking_Date, Booking_Class, Booking_Status, Trip_ID, Ticket_ID
- Passenger_ID → Passenger_Name, Phone_Number, Email_Address, Address
- Trip_ID → Trip_Date, Departure_Time, Arrival_Time, Route_ID, Bus_ID
- Route_ID → Origin, Destination, Distance_KM, Estimated_Duration
- Bus_ID → Bus_Registration_Number, Capacity, Bus_Type, Availability_Status
- Ticket_ID → Fare_Amount, Issue_Date, Payment_ID
- Payment_ID → Payment_Amount, Payment_Date, Payment_Method

For BUS_STAFF_1NF:
- Bus_ID → Bus_Registration_Number, Capacity, Bus_Type, Availability_Status
- Staff_ID → Staff_Name, Role, Staff_Phone, Hire_Date
- (Bus_ID, Staff_ID) → Assignment_Date

**Achievement:** All attributes now contain atomic values, and repeating groups have been eliminated.

### Second Normal Form (2NF)

**Objective:** Remove partial dependencies (attributes dependent on part of a composite key).

**Analysis of Partial Dependencies:**

In BUS_STAFF_1NF with composite key (Bus_ID, Staff_ID):
- Bus attributes depend only on Bus_ID (partial dependency)
- Staff attributes depend only on Staff_ID (partial dependency)
- Assignment_Date depends on the full composite key

**Decomposition to 2NF:**

**BUS_2NF**
```
(Bus_ID, Bus_Registration_Number, Capacity, Bus_Type, Availability_Status)
```
**Primary Key:** Bus_ID
**FD:** Bus_ID → Bus_Registration_Number, Capacity, Bus_Type, Availability_Status

**STAFF_2NF**
```
(Staff_ID, Staff_Name, Role, Staff_Phone, Hire_Date)
```
**Primary Key:** Staff_ID
**FD:** Staff_ID → Staff_Name, Role, Staff_Phone, Hire_Date

**BUS_STAFF_ASSIGNMENT_2NF**
```
(Bus_ID, Staff_ID, Assignment_Date)
```
**Primary Key:** (Bus_ID, Staff_ID) or Assignment_ID
**FD:** (Bus_ID, Staff_ID) → Assignment_Date

**For PASSENGER_BOOKING_1NF (has single attribute key, so already in 2NF):**

**PASSENGER_2NF**
```
(Passenger_ID, Passenger_Name, Phone_Number, Email_Address, Address)
```
**Primary Key:** Passenger_ID

**ROUTE_2NF**
```
(Route_ID, Origin, Destination, Distance_KM, Estimated_Duration)
```
**Primary Key:** Route_ID

**TRIP_2NF**
```
(Trip_ID, Route_ID, Bus_ID, Trip_Date, Departure_Time, Arrival_Time)
```
**Primary Key:** Trip_ID
**Foreign Keys:** Route_ID, Bus_ID

**BOOKING_2NF**
```
(Booking_ID, Passenger_ID, Trip_ID, Booking_Date, Booking_Class, Booking_Status)
```
**Primary Key:** Booking_ID
**Foreign Keys:** Passenger_ID, Trip_ID

**TICKET_2NF**
```
(Ticket_ID, Booking_ID, Fare_Amount, Issue_Date)
```
**Primary Key:** Ticket_ID
**Foreign Key:** Booking_ID

**PAYMENT_2NF**
```
(Payment_ID, Ticket_ID, Payment_Amount, Payment_Date, Payment_Method)
```
**Primary Key:** Payment_ID
**Foreign Key:** Ticket_ID

**Achievement:** All partial dependencies have been removed. Every non-key attribute is fully dependent on the entire primary key.

### Third Normal Form (3NF)

**Objective:** Remove transitive dependencies (non-key attributes depending on other non-key attributes).

**Analysis of Transitive Dependencies:**

Examining each 2NF relation:

1. **PASSENGER_2NF** - No transitive dependencies detected
2. **ROUTE_2NF** - No transitive dependencies detected
3. **BUS_2NF** - No transitive dependencies detected
4. **STAFF_2NF** - No transitive dependencies detected
5. **TRIP_2NF** - No transitive dependencies detected
6. **BOOKING_2NF** - No transitive dependencies detected
7. **TICKET_2NF** - No transitive dependencies detected
8. **PAYMENT_2NF** - No transitive dependencies detected
9. **BUS_STAFF_ASSIGNMENT_2NF** - No transitive dependencies detected

**Final 3NF Relations:**

**1. PASSENGER**
```
(Passenger_ID, Passenger_Name, Phone_Number, Email_Address, Address)
```
- **Primary Key:** Passenger_ID
- **FD:** Passenger_ID → Passenger_Name, Phone_Number, Email_Address, Address
- **3NF Proof:** All non-key attributes depend only on Passenger_ID (no transitive dependencies)

**2. ROUTE**
```
(Route_ID, Origin, Destination, Distance_KM, Estimated_Duration)
```
- **Primary Key:** Route_ID
- **FD:** Route_ID → Origin, Destination, Distance_KM, Estimated_Duration
- **3NF Proof:** All non-key attributes depend only on Route_ID

**3. BUS**
```
(Bus_ID, Bus_Registration_Number, Capacity, Bus_Type, Availability_Status)
```
- **Primary Key:** Bus_ID
- **FD:** Bus_ID → Bus_Registration_Number, Capacity, Bus_Type, Availability_Status
- **3NF Proof:** All non-key attributes depend only on Bus_ID

**4. STAFF**
```
(Staff_ID, Staff_Name, Role, Phone_Number, Hire_Date)
```
- **Primary Key:** Staff_ID
- **FD:** Staff_ID → Staff_Name, Role, Phone_Number, Hire_Date
- **3NF Proof:** All non-key attributes depend only on Staff_ID

**5. TRIP**
```
(Trip_ID, Route_ID, Bus_ID, Trip_Date, Departure_Time, Arrival_Time)
```
- **Primary Key:** Trip_ID
- **Foreign Keys:** Route_ID (references ROUTE), Bus_ID (references BUS)
- **FD:** Trip_ID → Route_ID, Bus_ID, Trip_Date, Departure_Time, Arrival_Time
- **3NF Proof:** All non-key attributes depend directly on Trip_ID

**6. BOOKING**
```
(Booking_ID, Passenger_ID, Trip_ID, Booking_Date, Booking_Class, Booking_Status)
```
- **Primary Key:** Booking_ID
- **Foreign Keys:** Passenger_ID (references PASSENGER), Trip_ID (references TRIP)
- **FD:** Booking_ID → Passenger_ID, Trip_ID, Booking_Date, Booking_Class, Booking_Status
- **3NF Proof:** All non-key attributes depend directly on Booking_ID

**7. TICKET**
```
(Ticket_ID, Booking_ID, Fare_Amount, Issue_Date)
```
- **Primary Key:** Ticket_ID
- **Foreign Key:** Booking_ID (references BOOKING)
- **FD:** Ticket_ID → Booking_ID, Fare_Amount, Issue_Date
- **3NF Proof:** All non-key attributes depend directly on Ticket_ID

**8. PAYMENT**
```
(Payment_ID, Ticket_ID, Payment_Amount, Payment_Date, Payment_Method)
```
- **Primary Key:** Payment_ID
- **Foreign Key:** Ticket_ID (references TICKET)
- **FD:** Payment_ID → Ticket_ID, Payment_Amount, Payment_Date, Payment_Method
- **3NF Proof:** All non-key attributes depend directly on Payment_ID

**9. BUS_STAFF_ASSIGNMENT**
```
(Assignment_ID, Bus_ID, Staff_ID, Assignment_Date)
```
- **Primary Key:** Assignment_ID
- **Foreign Keys:** Bus_ID (references BUS), Staff_ID (references STAFF)
- **FD:** Assignment_ID → Bus_ID, Staff_ID, Assignment_Date
- **3NF Proof:** All non-key attributes depend directly on Assignment_ID

**Total Entities after Normalization: 9 entities (exceeds minimum requirement of 8)**

**Summary of Normalization Process:**
- **UNF → 1NF:** Removed repeating groups and nested structures
- **1NF → 2NF:** Eliminated partial dependencies on composite keys
- **2NF → 3NF:** Verified no transitive dependencies exist
- **Result:** 9 well-structured tables in Third Normal Form

---

## Part 4: Data Dictionary and Final ERD (10%)

### 4.1 Data Dictionary

**Table 1: PASSENGER**
| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| Passenger_ID | NUMBER(10) | PRIMARY KEY | Unique identifier for passenger |
| Passenger_Name | VARCHAR2(100) | NOT NULL | Full name of passenger |
| Phone_Number | VARCHAR2(15) | NOT NULL, UNIQUE | Contact phone number |
| Email_Address | VARCHAR2(100) | NOT NULL, UNIQUE | Email address |
| Address | VARCHAR2(200) | NOT NULL | Residential address |

**Table 2: ROUTE**
| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| Route_ID | NUMBER(10) | PRIMARY KEY | Unique identifier for route |
| Origin | VARCHAR2(50) | NOT NULL | Starting city |
| Destination | VARCHAR2(50) | NOT NULL | Ending city |
| Distance_KM | NUMBER(6,2) | NOT NULL, CHECK > 0 | Distance in kilometers |
| Estimated_Duration | VARCHAR2(20) | NOT NULL | Estimated travel time |

**Table 3: BUS**
| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| Bus_ID | NUMBER(10) | PRIMARY KEY | Unique identifier for bus |
| Bus_Registration_Number | VARCHAR2(20) | NOT NULL, UNIQUE | Vehicle registration number |
| Capacity | NUMBER(3) | NOT NULL, CHECK > 0 | Seating capacity |
| Bus_Type | VARCHAR2(30) | NOT NULL | Type of bus (AC/Non-AC) |
| Availability_Status | VARCHAR2(20) | NOT NULL | Current status of bus |

**Table 4: STAFF**
| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| Staff_ID | NUMBER(10) | PRIMARY KEY | Unique identifier for staff |
| Staff_Name | VARCHAR2(100) | NOT NULL | Full name of staff member |
| Role | VARCHAR2(30) | NOT NULL | Job role (Driver/Conductor) |
| Phone_Number | VARCHAR2(15) | NOT NULL, UNIQUE | Contact phone number |
| Hire_Date | DATE | NOT NULL | Date of employment |

**Table 5: TRIP**
| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| Trip_ID | NUMBER(10) | PRIMARY KEY | Unique identifier for trip |
| Route_ID | NUMBER(10) | FOREIGN KEY | Reference to route |
| Bus_ID | NUMBER(10) | FOREIGN KEY | Reference to bus |
| Trip_Date | DATE | NOT NULL | Date of trip |
| Departure_Time | TIMESTAMP | NOT NULL | Departure date and time |
| Arrival_Time | TIMESTAMP | NOT NULL | Arrival date and time |

**Table 6: BOOKING**
| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| Booking_ID | NUMBER(10) | PRIMARY KEY | Unique identifier for booking |
| Passenger_ID | NUMBER(10) | FOREIGN KEY | Reference to passenger |
| Trip_ID | NUMBER(10) | FOREIGN KEY | Reference to trip |
| Booking_Date | DATE | NOT NULL | Date of booking |
| Booking_Class | VARCHAR2(20) | NOT NULL | Class type (Regular/Premium/VIP) |
| Booking_Status | VARCHAR2(20) | NOT NULL | Status (Confirmed/Cancelled/Pending) |

**Table 7: TICKET**
| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| Ticket_ID | NUMBER(10) | PRIMARY KEY | Unique identifier for ticket |
| Booking_ID | NUMBER(10) | FOREIGN KEY, UNIQUE | Reference to booking |
| Fare_Amount | NUMBER(8,2) | NOT NULL, CHECK > 0 | Ticket fare |
| Issue_Date | DATE | NOT NULL | Date ticket was issued |

**Table 8: PAYMENT**
| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| Payment_ID | NUMBER(10) | PRIMARY KEY | Unique identifier for payment |
| Ticket_ID | NUMBER(10) | FOREIGN KEY, UNIQUE | Reference to ticket |
| Payment_Amount | NUMBER(8,2) | NOT NULL, CHECK > 0 | Amount paid |
| Payment_Date | DATE | NOT NULL | Date of payment |
| Payment_Method | VARCHAR2(30) | NOT NULL | Payment method (Cash/Card/Online) |

**Table 9: BUS_STAFF_ASSIGNMENT**
| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| Assignment_ID | NUMBER(10) | PRIMARY KEY | Unique identifier for assignment |
| Bus_ID | NUMBER(10) | FOREIGN KEY | Reference to bus |
| Staff_ID | NUMBER(10) | FOREIGN KEY | Reference to staff |
| Assignment_Date | DATE | NOT NULL | Date of assignment |

### 4.2 Final Entity Relationship Diagram (After Normalization)

```
Final ERD Structure (3NF):

┌─────────────┐
│  PASSENGER  │
├─────────────┤
│ Passenger_ID│◄────┐
│ Name        │     │
│ Phone       │     │
│ Email       │     │ 1
│ Address     │     │
└─────────────┘     │
                    │
                    │ M
                ┌───┴──────┐
                │  BOOKING │
                ├──────────┤
                │Booking_ID│◄────┐
                │Passenger_│     │
                │ ID       │     │
                │Trip_ID   │     │ 1
                │Date      │     │
                │Class     │     │
                │Status    │     │
                └────┬─────┘     │
                     │           │
                     │ M         │
                     │           │
                     │           │ M
                ┌────▼─────┐    │
                │   TRIP   │    │
                ├──────────┤    │
                │ Trip_ID  │◄───┘
                │ Route_ID │◄────┐
                │ Bus_ID   │     │ M
                │ Date     │     │
                │ Dep_Time │     │
                │ Arr_Time │     │
                └──┬───────┘     │
                   │             │ 1
                   │ M       ┌───┴────┐
                   │         │ ROUTE  │
              1    │         ├────────┤
        ┌──────────▼─────┐   │Route_ID│
        │      BUS       │   │Origin  │
        ├────────────────┤   │Dest.   │
        │    Bus_ID      │   │Distance│
        │    Reg_Number  │   │Duration│
        │    Capacity    │   └────────┘
        │    Type        │
        │    Status      │
        └───┬────────────┘
            │
            │ M
            │
            │ M
     ┌──────▼──────────┐
     │ BUS_STAFF_      │
     │ ASSIGNMENT      │
     ├─────────────────┤
     │ Assignment_ID   │
     │ Bus_ID          │
     │ Staff_ID        │◄───┐
     │ Assign_Date     │    │
     └─────────────────┘    │ 1
                            │
                            │
                       ┌────┴────┐
                       │  STAFF  │
                       ├─────────┤
                       │Staff_ID │
                       │Name     │
                       │Role     │
                       │Phone    │
                       │Hire_Date│
                       └─────────┘

BOOKING to TICKET to PAYMENT Chain:

┌──────────┐ 1:1 ┌────────┐ 1:1 ┌─────────┐
│ BOOKING  ├─────┤ TICKET ├─────┤ PAYMENT │
├──────────┤     ├────────┤     ├─────────┤
│Booking_ID│     │Ticket_I│     │Payment_I│
│...       │     │Booking_│     │Ticket_ID│
└──────────┘     │ID      │     │Amount   │
                 │Fare    │     │Date     │
                 │Date    │     │Method   │
                 └────────┘     └─────────┘
```

**Relationship Summary:**
1. PASSENGER → BOOKING (1:M)
2. TRIP → BOOKING (1:M)
3. BOOKING → TICKET (1:1)
4. TICKET → PAYMENT (1:1)
5. ROUTE → TRIP (1:M)
6. BUS → TRIP (1:M)
7. BUS ↔ STAFF (M:M through BUS_STAFF_ASSIGNMENT)

**Cardinality Notations:**
- One passenger can make many bookings
- One trip can have many bookings
- One booking generates one ticket
- One ticket has one payment (optional until paid)
- One route has many trips
- One bus operates many trips
- Many buses can be assigned many staff members

---

## Part 5: Implementation (10%)

### 5.1 Create Relations and Tables (5 marks)

```sql
-- Create Table 1: PASSENGER
CREATE TABLE PASSENGER (
    Passenger_ID NUMBER(10) PRIMARY KEY,
    Passenger_Name VARCHAR2(100) NOT NULL,
    Phone_Number VARCHAR2(15) NOT NULL UNIQUE,
    Email_Address VARCHAR2(100) NOT NULL UNIQUE,
    Address VARCHAR2(200) NOT NULL
);

-- Create Table 2: ROUTE
CREATE TABLE ROUTE (
    Route_ID NUMBER(10) PRIMARY KEY,
    Origin VARCHAR2(50) NOT NULL,
    Destination VARCHAR2(50) NOT NULL,
    Distance_KM NUMBER(6,2) NOT NULL CHECK (Distance_KM > 0),
    Estimated_Duration VARCHAR2(20) NOT NULL
);

-- Create Table 3: BUS
CREATE TABLE BUS (
    Bus_ID NUMBER(10) PRIMARY KEY,
    Bus_Registration_Number VARCHAR2(20) NOT NULL UNIQUE,
    Capacity NUMBER(3) NOT NULL CHECK (Capacity > 0),
    Bus_Type VARCHAR2(30) NOT NULL,
    Availability_Status VARCHAR2(20) NOT NULL
);

-- Create Table 4: STAFF
CREATE TABLE STAFF (
    Staff_ID NUMBER(10) PRIMARY KEY,
    Staff_Name VARCHAR2(100) NOT NULL,
    Role VARCHAR2(30) NOT NULL,
    Phone_Number VARCHAR2(15) NOT NULL UNIQUE,
    Hire_Date DATE NOT NULL
);

-- Create Table 5: TRIP
CREATE TABLE TRIP (
    Trip_ID NUMBER(10) PRIMARY KEY,
    Route_ID NUMBER(10) NOT NULL,
    Bus_ID NUMBER(10) NOT NULL,
    Trip_Date DATE NOT NULL,
    Departure_Time TIMESTAMP NOT NULL,
    Arrival_Time TIMESTAMP NOT NULL,
    CONSTRAINT fk_trip_route FOREIGN KEY (Route_ID) REFERENCES ROUTE(Route_ID) ON DELETE CASCADE,
    CONSTRAINT fk_trip_bus FOREIGN KEY (Bus_ID) REFERENCES BUS(Bus_ID) ON DELETE CASCADE,
    CONSTRAINT chk_trip_time CHECK (Arrival_Time > Departure_Time)
);

-- Create Table 6: BOOKING
CREATE TABLE BOOKING (
    Booking_ID NUMBER(10) PRIMARY KEY,
    Passenger_ID NUMBER(10) NOT NULL,
    Trip_ID NUMBER(10) NOT NULL,
    Booking_Date DATE NOT NULL,
    Booking_Class VARCHAR2(20) NOT NULL CHECK (Booking_Class IN ('Regular', 'Premium', 'VIP')),
    Booking_Status VARCHAR2(20) NOT NULL CHECK (Booking_Status IN ('Confirmed', 'Cancelled', 'Pending')),
    CONSTRAINT fk_booking_passenger FOREIGN KEY (Passenger_ID) REFERENCES PASSENGER(Passenger_ID) ON DELETE CASCADE,
    CONSTRAINT fk_booking_trip FOREIGN KEY (Trip_ID) REFERENCES TRIP(Trip_ID) ON DELETE CASCADE
);

-- Create Table 7: TICKET
CREATE TABLE TICKET (
    Ticket_ID NUMBER(10) PRIMARY KEY,
    Booking_ID NUMBER(10) NOT NULL UNIQUE,
    Fare_Amount NUMBER(8,2) NOT NULL CHECK (Fare_Amount > 0),
    Issue_Date DATE NOT NULL,
    CONSTRAINT fk_ticket_booking FOREIGN KEY (Booking_ID) REFERENCES BOOKING(Booking_ID) ON DELETE CASCADE
);

-- Create Table 8: PAYMENT
CREATE TABLE PAYMENT (
    Payment_ID NUMBER(10) PRIMARY KEY,
    Ticket_ID NUMBER(10) NOT NULL UNIQUE,
    Payment_Amount NUMBER(8,2) NOT NULL CHECK (Payment_Amount > 0),
    Payment_Date DATE NOT NULL,
    Payment_Method VARCHAR2(30) NOT NULL CHECK (Payment_Method IN ('Cash', 'Card', 'Online', 'Mobile Banking')),
    CONSTRAINT fk_payment_ticket FOREIGN KEY (Ticket_ID) REFERENCES TICKET(Ticket_ID) ON DELETE CASCADE
);

-- Create Table 9: BUS_STAFF_ASSIGNMENT
CREATE TABLE BUS_STAFF_ASSIGNMENT (
    Assignment_ID NUMBER(10) PRIMARY KEY,
    Bus_ID NUMBER(10) NOT NULL,
    Staff_ID NUMBER(10) NOT NULL,
    Assignment_Date DATE NOT NULL,
    CONSTRAINT fk_assignment_bus FOREIGN KEY (Bus_ID) REFERENCES BUS(Bus_ID) ON DELETE CASCADE,
    CONSTRAINT fk_assignment_staff FOREIGN KEY (Staff_ID) REFERENCES STAFF(Staff_ID) ON DELETE CASCADE,
    CONSTRAINT uk_bus_staff UNIQUE (Bus_ID, Staff_ID, Assignment_Date)
);
```

**Screenshot Instructions:** Execute each CREATE TABLE statement in Oracle SQL*Plus and capture screenshots showing successful table creation.

### 5.2 Populate Tables with Test Data (5 marks)

```sql
-- Insert data into PASSENGER table (7+ rows)
INSERT INTO PASSENGER VALUES (1, 'Anil Sharma', '9841234567', 'anil.sharma@email.com', 'Kathmandu, Nepal');
INSERT INTO PASSENGER VALUES (2, 'Anjali Thapa', '9851234568', 'anjali.thapa@email.com', 'Pokhara, Nepal');
INSERT INTO PASSENGER VALUES (3, 'Arjun Gurung', '9861234569', 'arjun.gurung@email.com', 'Chitwan, Nepal');
INSERT INTO PASSENGER VALUES (4, 'Binita Rai', '9871234570', 'binita.rai@email.com', 'Butwal, Nepal');
INSERT INTO PASSENGER VALUES (5, 'Deepak Shrestha', '9881234571', 'deepak.shrestha@email.com', 'Kathmandu, Nepal');
INSERT INTO PASSENGER VALUES (6, 'Kabita Karki', '9891234572', 'kabita.karki@email.com', 'Pokhara, Nepal');
INSERT INTO PASSENGER VALUES (7, 'Rajesh Poudel', '9801234573', 'rajesh.poudel@email.com', 'Chitwan, Nepal');
COMMIT;

-- Insert data into ROUTE table (7+ rows)
INSERT INTO ROUTE VALUES (101, 'Kathmandu', 'Pokhara', 200.50, '6 hours');
INSERT INTO ROUTE VALUES (102, 'Pokhara', 'Chitwan', 150.75, '4 hours 30 min');
INSERT INTO ROUTE VALUES (103, 'Kathmandu', 'Chitwan', 145.20, '5 hours');
INSERT INTO ROUTE VALUES (104, 'Chitwan', 'Butwal', 120.00, '3 hours 45 min');
INSERT INTO ROUTE VALUES (105, 'Pokhara', 'Butwal', 125.50, '4 hours');
INSERT INTO ROUTE VALUES (106, 'Kathmandu', 'Butwal', 265.80, '8 hours');
INSERT INTO ROUTE VALUES (107, 'Butwal', 'Pokhara', 125.50, '4 hours');
COMMIT;

-- Insert data into BUS table (7+ rows)
INSERT INTO BUS VALUES (201, 'BA-1-PA-1234', 45, 'AC Deluxe', 'Available');
INSERT INTO BUS VALUES (202, 'BA-2-KHA-5678', 50, 'AC Standard', 'Available');
INSERT INTO BUS VALUES (203, 'BA-3-GA-9012', 40, 'Non-AC', 'Available');
INSERT INTO BUS VALUES (204, 'BA-1-NA-3456', 48, 'AC Deluxe', 'Maintenance');
INSERT INTO BUS VALUES (205, 'BA-2-CHA-7890', 52, 'AC Standard', 'Available');
INSERT INTO BUS VALUES (206, 'BA-3-JHA-2345', 45, 'Non-AC', 'Available');
INSERT INTO BUS VALUES (207, 'BA-1-TA-6789', 50, 'AC Deluxe', 'Available');
COMMIT;

-- Insert data into STAFF table (7+ rows)
INSERT INTO STAFF VALUES (301, 'Ram Bahadur Thapa', 'Driver', '9841111111', TO_DATE('2020-01-15', 'YYYY-MM-DD'));
INSERT INTO STAFF VALUES (302, 'Sita Kumari Sharma', 'Conductor', '9851111112', TO_DATE('2020-03-20', 'YYYY-MM-DD'));
INSERT INTO STAFF VALUES (303, 'Krishna Prasad Gautam', 'Driver', '9861111113', TO_DATE('2019-06-10', 'YYYY-MM-DD'));
INSERT INTO STAFF VALUES (304, 'Gita Devi Rai', 'Conductor', '9871111114', TO_DATE('2021-02-25', 'YYYY-MM-DD'));
INSERT INTO STAFF VALUES (305, 'Hari Bahadur Magar', 'Driver', '9881111115', TO_DATE('2018-09-05', 'YYYY-MM-DD'));
INSERT INTO STAFF VALUES (306, 'Maya Kumari Tamang', 'Conductor', '9891111116', TO_DATE('2021-07-18', 'YYYY-MM-DD'));
INSERT INTO STAFF VALUES (307, 'Bikram Singh Thakuri', 'Driver', '9801111117', TO_DATE('2019-11-30', 'YYYY-MM-DD'));
COMMIT;

-- Insert data into TRIP table (7+ rows)
INSERT INTO TRIP VALUES (401, 101, 201, TO_DATE('2025-12-15', 'YYYY-MM-DD'), 
    TO_TIMESTAMP('2025-12-15 06:00:00', 'YYYY-MM-DD HH24:MI:SS'), 
    TO_TIMESTAMP('2025-12-15 12:00:00', 'YYYY-MM-DD HH24:MI:SS'));
    
INSERT INTO TRIP VALUES (402, 102, 202, TO_DATE('2025-12-16', 'YYYY-MM-DD'), 
    TO_TIMESTAMP('2025-12-16 08:00:00', 'YYYY-MM-DD HH24:MI:SS'), 
    TO_TIMESTAMP('2025-12-16 12:30:00', 'YYYY-MM-DD HH24:MI:SS'));
    
INSERT INTO TRIP VALUES (403, 103, 203, TO_DATE('2025-12-17', 'YYYY-MM-DD'), 
    TO_TIMESTAMP('2025-12-17 07:00:00', 'YYYY-MM-DD HH24:MI:SS'), 
    TO_TIMESTAMP('2025-12-17 12:00:00', 'YYYY-MM-DD HH24:MI:SS'));
    
INSERT INTO TRIP VALUES (404, 104, 205, TO_DATE('2025-12-18', 'YYYY-MM-DD'), 
    TO_TIMESTAMP('2025-12-18 09:00:00', 'YYYY-MM-DD HH24:MI:SS'), 
    TO_TIMESTAMP('2025-12-18 12:45:00', 'YYYY-MM-DD HH24:MI:SS'));
    
INSERT INTO TRIP VALUES (405, 105, 206, TO_DATE('2025-12-20', 'YYYY-MM-DD'), 
    TO_TIMESTAMP('2025-12-20 10:00:00', 'YYYY-MM-DD HH24:MI:SS'), 
    TO_TIMESTAMP('2025-12-20 14:00:00', 'YYYY-MM-DD HH24:MI:SS'));
    
INSERT INTO TRIP VALUES (406, 106, 207, TO_DATE('2025-12-22', 'YYYY-MM-DD'), 
    TO_TIMESTAMP('2025-12-22 05:00:00', 'YYYY-MM-DD HH24:MI:SS'), 
    TO_TIMESTAMP('2025-12-22 13:00:00', 'YYYY-MM-DD HH24:MI:SS'));
    
INSERT INTO TRIP VALUES (407, 101, 201, TO_DATE('2025-12-25', 'YYYY-MM-DD'), 
    TO_TIMESTAMP('2025-12-25 14:00:00', 'YYYY-MM-DD HH24:MI:SS'), 
    TO_TIMESTAMP('2025-12-25 20:00:00', 'YYYY-MM-DD HH24:MI:SS'));
COMMIT;

-- Insert data into BOOKING table (7+ rows)
INSERT INTO BOOKING VALUES (501, 1, 401, TO_DATE('2025-12-10', 'YYYY-MM-DD'), 'Premium', 'Confirmed');
INSERT INTO BOOKING VALUES (502, 2, 401, TO_DATE('2025-12-11', 'YYYY-MM-DD'), 'VIP', 'Confirmed');
INSERT INTO BOOKING VALUES (503, 3, 402, TO_DATE('2025-12-12', 'YYYY-MM-DD'), 'Regular', 'Confirmed');
INSERT INTO BOOKING VALUES (504, 4, 403, TO_DATE('2025-12-13', 'YYYY-MM-DD'), 'Premium', 'Confirmed');
INSERT INTO BOOKING VALUES (505, 1, 404, TO_DATE('2025-12-14', 'YYYY-MM-DD'), 'Regular', 'Confirmed');
INSERT INTO BOOKING VALUES (506, 2, 405, TO_DATE('2025-12-15', 'YYYY-MM-DD'), 'VIP', 'Confirmed');
INSERT INTO BOOKING VALUES (507, 3, 406, TO_DATE('2025-12-16', 'YYYY-MM-DD'), 'Premium', 'Cancelled');
COMMIT;

-- Insert data into TICKET table (7+ rows)
INSERT INTO TICKET VALUES (601, 501, 1500.00, TO_DATE('2025-12-10', 'YYYY-MM-DD'));
INSERT INTO TICKET VALUES (602, 502, 2500.00, TO_DATE('2025-12-11', 'YYYY-MM-DD'));
INSERT INTO TICKET VALUES (603, 503, 800.00, TO_DATE('2025-12-12', 'YYYY-MM-DD'));
INSERT INTO TICKET VALUES (604, 504, 1200.00, TO_DATE('2025-12-13', 'YYYY-MM-DD'));
INSERT INTO TICKET VALUES (605, 505, 750.00, TO_DATE('2025-12-14', 'YYYY-MM-DD'));
INSERT INTO TICKET VALUES (606, 506, 2000.00, TO_DATE('2025-12-15', 'YYYY-MM-DD'));
INSERT INTO TICKET VALUES (607, 507, 1800.00, TO_DATE('2025-12-16', 'YYYY-MM-DD'));
COMMIT;

-- Insert data into PAYMENT table (7+ rows)
INSERT INTO PAYMENT VALUES (701, 601, 1500.00, TO_DATE('2025-12-10', 'YYYY-MM-DD'), 'Online');
INSERT INTO PAYMENT VALUES (702, 602, 2500.00, TO_DATE('2025-12-11', 'YYYY-MM-DD'), 'Card');
INSERT INTO PAYMENT VALUES (703, 603, 800.00, TO_DATE('2025-12-12', 'YYYY-MM-DD'), 'Cash');
INSERT INTO PAYMENT VALUES (704, 604, 1200.00, TO_DATE('2025-12-13', 'YYYY-MM-DD'), 'Mobile Banking');
INSERT INTO PAYMENT VALUES (705, 605, 750.00, TO_DATE('2025-12-14', 'YYYY-MM-DD'), 'Online');
INSERT INTO PAYMENT VALUES (706, 606, 2000.00, TO_DATE('2025-12-15', 'YYYY-MM-DD'), 'Card');
INSERT INTO PAYMENT VALUES (707, 607, 1800.00, TO_DATE('2025-12-16', 'YYYY-MM-DD'), 'Cash');
COMMIT;

-- Insert data into BUS_STAFF_ASSIGNMENT table (7+ rows)
INSERT INTO BUS_STAFF_ASSIGNMENT VALUES (801, 201, 301, TO_DATE('2025-12-15', 'YYYY-MM-DD'));
INSERT INTO BUS_STAFF_ASSIGNMENT VALUES (802, 201, 302, TO_DATE('2025-12-15', 'YYYY-MM-DD'));
INSERT INTO BUS_STAFF_ASSIGNMENT VALUES (803, 202, 303, TO_DATE('2025-12-16', 'YYYY-MM-DD'));
INSERT INTO BUS_STAFF_ASSIGNMENT VALUES (804, 202, 304, TO_DATE('2025-12-16', 'YYYY-MM-DD'));
INSERT INTO BUS_STAFF_ASSIGNMENT VALUES (805, 203, 305, TO_DATE('2025-12-17', 'YYYY-MM-DD'));
INSERT INTO BUS_STAFF_ASSIGNMENT VALUES (806, 203, 306, TO_DATE('2025-12-17', 'YYYY-MM-DD'));
INSERT INTO BUS_STAFF_ASSIGNMENT VALUES (807, 205, 307, TO_DATE('2025-12-18', 'YYYY-MM-DD'));
COMMIT;

-- Verify data insertion
SELECT * FROM PASSENGER;
SELECT * FROM ROUTE;
SELECT * FROM BUS;
SELECT * FROM STAFF;
SELECT * FROM TRIP;
SELECT * FROM BOOKING;
SELECT * FROM TICKET;
SELECT * FROM PAYMENT;
SELECT * FROM BUS_STAFF_ASSIGNMENT;
```

**Screenshot Instructions:** Execute all INSERT statements and SELECT statements, capturing screenshots of both the SQL commands and the resulting table contents.

---

## Part 6: Database Querying (25%)

### 6.1 Information Queries (10 marks)

**Query 1: List all routes along with the total number of trips scheduled on each route**

```sql
SELECT 
    R.Route_ID,
    R.Origin,
    R.Destination,
    COUNT(T.Trip_ID) AS Total_Trips
FROM 
    ROUTE R
LEFT JOIN 
    TRIP T ON R.Route_ID = T.Route_ID
GROUP BY 
    R.Route_ID, R.Origin, R.Destination
ORDER BY 
    Total_Trips DESC;
```

**Purpose:** This query provides a summary of trip distribution across all routes, helping management understand which routes are most frequently scheduled.

---

**Query 2: List all trips departing from "Pokhara" with their departure time and assigned route name**

```sql
SELECT 
    T.Trip_ID,
    R.Origin || ' to ' || R.Destination AS Route_Name,
    T.Trip_Date,
    TO_CHAR(T.Departure_Time, 'DD-MON-YYYY HH24:MI:SS') AS Departure_Time
FROM 
    TRIP T
JOIN 
    ROUTE R ON T.Route_ID = R.Route_ID
WHERE 
    R.Origin = 'Pokhara'
ORDER BY 
    T.Departure_Time;
```

**Purpose:** This query identifies all trips originating from Pokhara, useful for passengers and staff planning travel from that city.

---

**Query 3: List the names of passengers whose names start with 'A', along with the total number of trips they have booked**

```sql
SELECT 
    P.Passenger_Name,
    P.Phone_Number,
    COUNT(B.Booking_ID) AS Total_Trips_Booked
FROM 
    PASSENGER P
JOIN 
    BOOKING B ON P.Passenger_ID = B.Passenger_ID
WHERE 
    P.Passenger_Name LIKE 'A%'
GROUP BY 
    P.Passenger_Name, P.Phone_Number
ORDER BY 
    Total_Trips_Booked DESC;
```

**Purpose:** This query filters passengers whose names start with 'A' and shows their booking frequency, useful for targeted marketing or customer analysis.

---

**Query 4: List all passengers who have booked more than 2 trips in December 2025**

```sql
SELECT 
    P.Passenger_ID,
    P.Passenger_Name,
    P.Email_Address,
    COUNT(B.Booking_ID) AS Total_Bookings_Dec2025
FROM 
    PASSENGER P
JOIN 
    BOOKING B ON P.Passenger_ID = B.Passenger_ID
WHERE 
    B.Booking_Date >= TO_DATE('2025-12-01', 'YYYY-MM-DD')
    AND B.Booking_Date < TO_DATE('2026-01-01', 'YYYY-MM-DD')
GROUP BY 
    P.Passenger_ID, P.Passenger_Name, P.Email_Address
HAVING 
    COUNT(B.Booking_ID) > 2
ORDER BY 
    Total_Bookings_Dec2025 DESC;
```

**Purpose:** Identifies frequent travelers in December 2025, useful for loyalty programs or special offers to high-volume customers.

---

**Query 5: List all tickets issued in January 2025 with passenger names, trip IDs, and payment status ('Paid' or 'Unpaid')**

```sql
SELECT 
    T.Ticket_ID,
    P.Passenger_Name,
    B.Trip_ID,
    T.Fare_Amount,
    TO_CHAR(T.Issue_Date, 'DD-MON-YYYY') AS Issue_Date,
    CASE 
        WHEN PAY.Payment_ID IS NOT NULL THEN 'Paid'
        ELSE 'Unpaid'
    END AS Payment_Status
FROM 
    TICKET T
JOIN 
    BOOKING B ON T.Booking_ID = B.Booking_ID
JOIN 
    PASSENGER P ON B.Passenger_ID = P.Passenger_ID
LEFT JOIN 
    PAYMENT PAY ON T.Ticket_ID = PAY.Ticket_ID
WHERE 
    T.Issue_Date >= TO_DATE('2025-01-01', 'YYYY-MM-DD')
    AND T.Issue_Date < TO_DATE('2025-02-01', 'YYYY-MM-DD')
ORDER BY 
    T.Issue_Date;
```

**Purpose:** Tracks ticket issuance and payment status for January 2025, helping accounts department identify unpaid tickets.

---

### 6.2 Transaction Queries (15 marks)

**Query 1: Find the trip with the latest departure time**

```sql
SELECT 
    T.Trip_ID,
    R.Origin || ' to ' || R.Destination AS Route,
    TO_CHAR(T.Departure_Time, 'DD-MON-YYYY HH24:MI:SS') AS Latest_Departure_Time,
    B.Bus_Registration_Number
FROM 
    TRIP T
JOIN 
    ROUTE R ON T.Route_ID = R.Route_ID
JOIN 
    BUS B ON T.Bus_ID = B.Bus_ID
WHERE 
    T.Departure_Time = (SELECT MAX(Departure_Time) FROM TRIP);
```

**Purpose:** Identifies the last scheduled trip, useful for operational planning and ensuring coverage throughout the day.

---

**Query 2: List the top three passengers who have booked the most trips**

```sql
SELECT * FROM (
    SELECT 
        P.Passenger_ID,
        P.Passenger_Name,
        P.Email_Address,
        COUNT(B.Booking_ID) AS Total_Trips_Booked
    FROM 
        PASSENGER P
    JOIN 
        BOOKING B ON P.Passenger_ID = B.Passenger_ID
    GROUP BY 
        P.Passenger_ID, P.Passenger_Name, P.Email_Address
    ORDER BY 
        Total_Trips_Booked DESC
)
WHERE ROWNUM <= 3;
```

**Purpose:** Identifies top customers for VIP treatment, loyalty rewards, or retention strategies.

---

**Query 3: List all passengers who have made payments greater than the average payment amount, along with the total amount they have paid**

```sql
SELECT 
    P.Passenger_ID,
    P.Passenger_Name,
    SUM(PAY.Payment_Amount) AS Total_Amount_Paid,
    COUNT(PAY.Payment_ID) AS Number_of_Payments
FROM 
    PASSENGER P
JOIN 
    BOOKING B ON P.Passenger_ID = B.Passenger_ID
JOIN 
    TICKET T ON B.Booking_ID = T.Booking_ID
JOIN 
    PAYMENT PAY ON T.Ticket_ID = PAY.Ticket_ID
WHERE 
    PAY.Payment_Amount > (SELECT AVG(Payment_Amount) FROM PAYMENT)
GROUP BY 
    P.Passenger_ID, P.Passenger_Name
ORDER BY 
    Total_Amount_Paid DESC;
```

**Purpose:** Identifies high-value customers who spend more than average, useful for premium service offerings.

---

**Query 4: Calculate total revenue generated per route along with the number of trips operated on each route**

```sql
SELECT 
    R.Route_ID,
    R.Origin || ' to ' || R.Destination AS Route_Name,
    COUNT(DISTINCT T.Trip_ID) AS Total_Trips_Operated,
    NVL(SUM(PAY.Payment_Amount), 0) AS Total_Revenue
FROM 
    ROUTE R
LEFT JOIN 
    TRIP T ON R.Route_ID = T.Route_ID
LEFT JOIN 
    BOOKING B ON T.Trip_ID = B.Trip_ID
LEFT JOIN 
    TICKET TK ON B.Booking_ID = TK.Booking_ID
LEFT JOIN 
    PAYMENT PAY ON TK.Ticket_ID = PAY.Ticket_ID
GROUP BY 
    R.Route_ID, R.Origin, R.Destination
ORDER BY 
    Total_Revenue DESC;
```

**Purpose:** Provides financial analysis showing which routes are most profitable, guiding business expansion decisions.

---

**Query 5: List all trips where the number of booked tickets is less than 50% of the bus capacity**

```sql
SELECT 
    T.Trip_ID,
    R.Origin || ' to ' || R.Destination AS Route,
    TO_CHAR(T.Departure_Time, 'DD-MON-YYYY HH24:MI:SS') AS Departure_Time,
    B.Bus_Registration_Number,
    B.Capacity AS Bus_Capacity,
    COUNT(BK.Booking_ID) AS Tickets_Booked,
    ROUND((COUNT(BK.Booking_ID) / B.Capacity) * 100, 2) AS Occupancy_Percentage
FROM 
    TRIP T
JOIN 
    ROUTE R ON T.Route_ID = R.Route_ID
JOIN 
    BUS B ON T.Bus_ID = B.Bus_ID
LEFT JOIN 
    BOOKING BK ON T.Trip_ID = BK.Trip_ID
GROUP BY 
    T.Trip_ID, R.Origin, R.Destination, T.Departure_Time, 
    B.Bus_Registration_Number, B.Capacity
HAVING 
    COUNT(BK.Booking_ID) < (B.Capacity * 0.5)
ORDER BY 
    Occupancy_Percentage;
```

**Purpose:** Identifies under-utilized trips that may need marketing efforts, schedule adjustments, or route optimization.

---

## Part 7: Critical Evaluation (5%)

### 7.1 Critical Evaluation of Module and Its Relation with Other Subjects

The **CC5051 Databases** module serves as a foundational pillar for computer science and information technology education, providing essential knowledge that interconnects with multiple related disciplines:

**Relationship with Programming and Software Development:**
Database concepts directly complement programming courses. Understanding SQL and relational database management enables developers to create data-driven applications. The normalization principles learned in this module prevent redundancy and improve application performance. Object-oriented programming courses benefit from database knowledge when implementing persistence layers and ORM (Object-Relational Mapping) frameworks.

**Integration with Systems Analysis and Design:**
This module reinforces concepts from systems analysis courses. The process of identifying entities, attributes, and relationships mirrors requirements gathering and analysis phases in software development lifecycle. ERD creation skills directly support system design documentation and stakeholder communication.

**Connection to Data Structures and Algorithms:**
Database indexing strategies relate to data structure concepts like B-trees and hash tables. Query optimization connects to algorithm efficiency and complexity analysis. Understanding these relationships helps students appreciate practical applications of theoretical computer science concepts.

**Relevance to Web Development:**
Modern web applications rely heavily on database backends. Knowledge from this module enables students to design robust database schemas for e-commerce, social media, and enterprise web applications. Understanding transaction management and ACID properties becomes crucial for maintaining data integrity in multi-user web environments.

**Foundation for Advanced Topics:**
This module prepares students for advanced subjects including:
- Data Warehousing and Business Intelligence
- Big Data Analytics and NoSQL databases
- Database Administration and Performance Tuning
- Cloud Database Services (AWS RDS, Azure SQL)

**Real-World Applicability:**
The SajiloYatra case study demonstrates practical application of database concepts to solve real business problems. This bridges the gap between theoretical knowledge and industry requirements, preparing students for professional software development roles.

### 7.2 Critical Assessment of Coursework

**Strengths of the Coursework:**

1. **Comprehensive Coverage**: The coursework effectively covers all essential database concepts from conceptual design (ERD) through normalization to physical implementation and querying.

2. **Practical Relevance**: The SajiloYatra case study represents a realistic business scenario with complex relationships, making the learning experience applicable to real-world situations in Nepal's transportation sector.

3. **Progressive Learning**: The milestone structure allows incremental learning and feedback, reducing overwhelming workload and enabling better understanding of each phase.

4. **Skill Development**: The coursework develops multiple competencies including analytical thinking (normalization), design skills (ERD creation), technical proficiency (SQL), and documentation abilities.

5. **Query Complexity Gradation**: The division between information queries and transaction queries appropriately challenges students with increasing complexity levels.

**Areas for Improvement:**

1. **Tool Restriction**: Mandating Oracle SQL*Plus exclusively limits exposure to other popular database systems like PostgreSQL, MySQL, or cloud-based solutions that students may encounter professionally.

2. **Limited Database Features**: The coursework could include advanced topics such as triggers, stored procedures, views, and indexes to provide more comprehensive database programming experience.

3. **Testing Requirements**: The coursework lacks emphasis on data validation testing, edge case handling, and error management which are crucial for production databases.

4. **Performance Considerations**: No requirements for query optimization analysis or execution plan evaluation, which are important skills for database developers.

5. **Security Aspects**: The coursework doesn't address database security, user privileges, or role-based access control which are critical in enterprise environments.

**Suggestions for Enhancement:**

- Include a requirement for creating views for frequently accessed query patterns
- Add stored procedures for complex business logic
- Incorporate backup and recovery procedures
- Include performance benchmarking of queries with EXPLAIN PLAN
- Add requirements for handling concurrent transactions and deadlock scenarios

**Overall Assessment:**
Despite minor areas for improvement, this coursework provides a solid foundation in database design and implementation. The structured approach from conceptual modeling to query writing effectively builds essential database management skills required in the IT industry.

---

## Part 8: Structure and Formatting (5%)

This coursework document has been structured with:
- Clear section headings and subheadings
- Proper table formatting for data dictionaries
- Consistent SQL code formatting with indentation
- Logical flow from theory to practical implementation
- Professional presentation suitable for academic submission
- Comprehensive explanations for each component
- Proper citation of business rules and constraints

---

## Part 9: Drop Query and Database Dump File Creation (5%)

### 9.1 Create Database Dump File (2 marks)

**Instructions for Creating Dump File:**

**Step 1: Create Directory for Dump File (if not exists)**
```sql
-- Connect as SYSTEM or privileged user
CREATE OR REPLACE DIRECTORY dump_dir AS 'C:\oracle\dumps';
GRANT READ, WRITE ON DIRECTORY dump_dir TO your_username;
```

**Step 2: Export Database Using Data Pump**

From Command Prompt/Terminal (not SQL*Plus):
```bash
expdp username/password@database_name 
    DIRECTORY=dump_dir 
    DUMPFILE=sajiloyatra_db.dmp 
    LOGFILE=sajiloyatra_export.log 
    SCHEMAS=your_schema_name 
    TABLES=PASSENGER,ROUTE,BUS,STAFF,TRIP,BOOKING,TICKET,PAYMENT,BUS_STAFF_ASSIGNMENT
```

**Alternative Method: Using Traditional Export Utility**
```bash
exp username/password@database_name 
    FILE=sajiloyatra_db.dmp 
    LOG=sajiloyatra_export.log 
    OWNER=your_schema_name 
    TABLES=(PASSENGER,ROUTE,BUS,STAFF,TRIP,BOOKING,TICKET,PAYMENT,BUS_STAFF_ASSIGNMENT)
```

**Screenshot Instructions:**
1. Capture screenshot of the export command execution
2. Capture screenshot showing successful completion message
3. Capture screenshot of the created .dmp file in the directory
4. Include the log file content showing export statistics

**Expected Output:**
```
Export: Release 12.2.0.1.0 - Production on [Date]
Copyright (c) 1982, 2017, Oracle and/or its affiliates. All rights reserved.

Connected to: Oracle Database 12c Enterprise Edition Release 12.2.0.1.0 - 64bit Production

Starting "USERNAME"."SYS_EXPORT_TABLE_01": username/******** directory=dump_dir...
Processing object type TABLE_EXPORT/TABLE/TABLE_DATA
Processing object type TABLE_EXPORT/TABLE/STATISTICS/TABLE_STATISTICS
Processing object type TABLE_EXPORT/TABLE/CONSTRAINT/CONSTRAINT
Processing object type TABLE_EXPORT/TABLE/INDEX/INDEX
Processing object type TABLE_EXPORT/TABLE/CONSTRAINT/REF_CONSTRAINT

. . exported "PASSENGER"                         [XX] KB      7 rows
. . exported "ROUTE"                              [XX] KB      7 rows
. . exported "BUS"                                [XX] KB      7 rows
. . exported "STAFF"                              [XX] KB      7 rows
. . exported "TRIP"                               [XX] KB      7 rows
. . exported "BOOKING"                            [XX] KB      7 rows
. . exported "TICKET"                             [XX] KB      7 rows
. . exported "PAYMENT"                            [XX] KB      7 rows
. . exported "BUS_STAFF_ASSIGNMENT"               [XX] KB      7 rows

Master table "USERNAME"."SYS_EXPORT_TABLE_01" successfully loaded/unloaded
******************************************************************************
Dump file set for USERNAME.SYS_EXPORT_TABLE_01 is:
  C:\ORACLE\DUMPS\SAJILOYATRA_DB.DMP
Job "USERNAME"."SYS_EXPORT_TABLE_01" successfully completed
```

### 9.2 Drop Tables in Correct Order (3 marks)

**Important:** Tables must be dropped in reverse order of dependencies to avoid foreign key constraint violations.

```sql
-- ============================================================
-- DROP TABLES IN CORRECT ORDER (REVERSE OF DEPENDENCIES)
-- ============================================================

-- Step 1: Drop tables that have foreign keys referencing other tables
-- (Child tables first, then parent tables)

-- Drop BUS_STAFF_ASSIGNMENT (references BUS and STAFF)
DROP TABLE BUS_STAFF_ASSIGNMENT CASCADE CONSTRAINTS;

-- Drop PAYMENT (references TICKET)
DROP TABLE PAYMENT CASCADE CONSTRAINTS;

-- Drop TICKET (references BOOKING)
DROP TABLE TICKET CASCADE CONSTRAINTS;

-- Drop BOOKING (references PASSENGER and TRIP)
DROP TABLE BOOKING CASCADE CONSTRAINTS;

-- Drop TRIP (references ROUTE and BUS)
DROP TABLE TRIP CASCADE CONSTRAINTS;

-- Drop STAFF (no dependencies from other tables)
DROP TABLE STAFF CASCADE CONSTRAINTS;

-- Drop BUS (no dependencies from other tables after TRIP is dropped)
DROP TABLE BUS CASCADE CONSTRAINTS;

-- Drop ROUTE (no dependencies from other tables after TRIP is dropped)
DROP TABLE ROUTE CASCADE CONSTRAINTS;

-- Drop PASSENGER (no dependencies from other tables after BOOKING is dropped)
DROP TABLE PASSENGER CASCADE CONSTRAINTS;

-- Verify all tables have been dropped
SELECT table_name FROM user_tables;

-- Expected output: no rows selected (or empty result set)
```

**Alternative: Drop All Tables Using CASCADE CONSTRAINTS (Simpler Method)**

```sql
-- ============================================================
-- ALTERNATIVE METHOD: DROP WITH CASCADE CONSTRAINTS
-- ============================================================
-- This method automatically handles foreign key dependencies

DROP TABLE PASSENGER CASCADE CONSTRAINTS;
DROP TABLE ROUTE CASCADE CONSTRAINTS;
DROP TABLE BUS CASCADE CONSTRAINTS;
DROP TABLE STAFF CASCADE CONSTRAINTS;
DROP TABLE TRIP CASCADE CONSTRAINTS;
DROP TABLE BOOKING CASCADE CONSTRAINTS;
DROP TABLE TICKET CASCADE CONSTRAINTS;
DROP TABLE PAYMENT CASCADE CONSTRAINTS;
DROP TABLE BUS_STAFF_ASSIGNMENT CASCADE CONSTRAINTS;

-- Verify all tables are dropped
SELECT table_name FROM user_tables 
WHERE table_name IN ('PASSENGER','ROUTE','BUS','STAFF','TRIP',
                     'BOOKING','TICKET','PAYMENT','BUS_STAFF_ASSIGNMENT');
```

**Screenshot Instructions:**
1. Execute each DROP TABLE statement
2. Capture screenshot of successful execution for each DROP command
3. Capture screenshot of verification query showing no tables remain
4. Show timestamp/execution time for documentation

**Explanation of Drop Order:**

**Dependency Chain:**
```
Level 4 (Most Dependent - Drop First):
├── PAYMENT (depends on TICKET)
└── BUS_STAFF_ASSIGNMENT (depends on BUS and STAFF)

Level 3:
└── TICKET (depends on BOOKING)

Level 2:
├── BOOKING (depends on PASSENGER and TRIP)

Level 1:
└── TRIP (depends on ROUTE and BUS)

Level 0 (Independent - Drop Last):
├── PASSENGER
├── ROUTE
├── BUS
└── STAFF
```

**Why This Order Matters:**
1. **Foreign Key Integrity**: Dropping a parent table before its child tables would violate referential integrity constraints
2. **Cascade Constraints**: Using CASCADE CONSTRAINTS automatically drops related constraints, but proper order is still best practice
3. **Clean Database**: Ensures complete removal without orphaned constraints or indexes

**Verification After Drop:**

```sql
-- Check for any remaining tables
SELECT table_name, tablespace_name 
FROM user_tables
ORDER BY table_name;

-- Check for any remaining constraints
SELECT constraint_name, table_name, constraint_type
FROM user_constraints
WHERE table_name IN ('PASSENGER','ROUTE','BUS','STAFF','TRIP',
                     'BOOKING','TICKET','PAYMENT','BUS_STAFF_ASSIGNMENT');

-- Check for any remaining indexes
SELECT index_name, table_name
FROM user_indexes
WHERE table_name IN ('PASSENGER','ROUTE','BUS','STAFF','TRIP',
                     'BOOKING','TICKET','PAYMENT','BUS_STAFF_ASSIGNMENT');

-- All queries above should return no rows if cleanup was successful
```

**Complete Drop Script with Comments:**

```sql
-- ============================================================
-- SAJILOYATRA DATABASE - COMPLETE DROP SCRIPT
-- Author: [Your Name]
-- Date: [Current Date]
-- Purpose: Clean removal of all SajiloYatra database objects
-- ============================================================

SET ECHO ON
SET FEEDBACK ON
SPOOL drop_tables_log.txt

-- Display timestamp
SELECT 'Starting table drop process at: ' || TO_CHAR(SYSDATE, 'DD-MON-YYYY HH24:MI:SS') AS STATUS FROM DUAL;

-- Display existing tables before drop
SELECT 'Tables before drop:' AS STATUS FROM DUAL;
SELECT table_name FROM user_tables 
WHERE table_name IN ('PASSENGER','ROUTE','BUS','STAFF','TRIP',
                     'BOOKING','TICKET','PAYMENT','BUS_STAFF_ASSIGNMENT')
ORDER BY table_name;

-- Drop tables in dependency order
PROMPT Dropping BUS_STAFF_ASSIGNMENT table...
DROP TABLE BUS_STAFF_ASSIGNMENT CASCADE CONSTRAINTS;

PROMPT Dropping PAYMENT table...
DROP TABLE PAYMENT CASCADE CONSTRAINTS;

PROMPT Dropping TICKET table...
DROP TABLE TICKET CASCADE CONSTRAINTS;

PROMPT Dropping BOOKING table...
DROP TABLE BOOKING CASCADE CONSTRAINTS;

PROMPT Dropping TRIP table...
DROP TABLE TRIP CASCADE CONSTRAINTS;

PROMPT Dropping STAFF table...
DROP TABLE STAFF CASCADE CONSTRAINTS;

PROMPT Dropping BUS table...
DROP TABLE BUS CASCADE CONSTRAINTS;

PROMPT Dropping ROUTE table...
DROP TABLE ROUTE CASCADE CONSTRAINTS;

PROMPT Dropping PASSENGER table...
DROP TABLE PASSENGER CASCADE CONSTRAINTS;

-- Verify all tables are dropped
SELECT 'Tables after drop:' AS STATUS FROM DUAL;
SELECT table_name FROM user_tables 
WHERE table_name IN ('PASSENGER','ROUTE','BUS','STAFF','TRIP',
                     'BOOKING','TICKET','PAYMENT','BUS_STAFF_ASSIGNMENT')
ORDER BY table_name;

-- Display completion timestamp
SELECT 'Table drop process completed at: ' || TO_CHAR(SYSDATE, 'DD-MON-YYYY HH24:MI:SS') AS STATUS FROM DUAL;

SPOOL OFF
SET ECHO OFF

-- Expected output: "no rows selected" for final verification query
```

**Expected Console Output:**

```
Starting table drop process at: 20-NOV-2025 15:30:45

Tables before drop:
TABLE_NAME
------------------------------
BOOKING
BUS
BUS_STAFF_ASSIGNMENT
PASSENGER
PAYMENT
ROUTE
STAFF
TICKET
TRIP

9 rows selected.

Dropping BUS_STAFF_ASSIGNMENT table...
Table dropped.

Dropping PAYMENT table...
Table dropped.

Dropping TICKET table...
Table dropped.

Dropping BOOKING table...
Table dropped.

Dropping TRIP table...
Table dropped.

Dropping STAFF table...
Table dropped.

Dropping BUS table...
Table dropped.

Dropping ROUTE table...
Table dropped.

Dropping PASSENGER table...
Table dropped.

Tables after drop:
no rows selected

Table drop process completed at: 20-NOV-2025 15:31:12
```

---

## Part 10: Viva Preparation Guidelines

### Key Topics to Prepare:

**1. Database Design Concepts**
- Explain your entity identification process
- Justify your attribute selection for each entity
- Describe cardinality decisions in relationships
- Explain primary and foreign key selections

**2. Normalization Understanding**
- Explain each normal form with examples from your database
- Demonstrate functional dependencies
- Justify why your tables are in 3NF
- Discuss any denormalization decisions (if applicable)

**3. SQL Query Explanation**
- Explain the logic behind each query
- Discuss alternative query approaches
- Explain JOIN operations used
- Describe aggregate functions and their purposes

**4. Implementation Decisions**
- Justify data type selections
- Explain constraint implementations
- Discuss referential integrity enforcement
- Describe index considerations (if added)

**5. Business Logic**
- Explain how your database supports SajiloYatra operations
- Discuss how business rules are enforced
- Describe transaction scenarios
- Explain data integrity measures

**6. Critical Thinking Questions**
- How would you scale this database for 100,000 daily users?
- What additional features would improve the system?
- How would you handle concurrent bookings for the same seat?
- What backup and recovery strategy would you implement?

### Sample Viva Questions and Answers:

**Q: Why did you normalize to 3NF specifically?**
A: Third Normal Form eliminates transitive dependencies and most redundancy while maintaining practical query performance. It balances normalization benefits with real-world usability. Going beyond 3NF (BCNF, 4NF) would add complexity without significant benefit for this use case.

**Q: How does your database prevent double-booking?**
A: The BOOKING table links each passenger to a specific trip through unique booking IDs. To fully prevent double-booking of the same seat, we would need a SEAT table with seat numbers and a constraint ensuring one booking per seat per trip.

**Q: Explain the difference between UNIQUE and PRIMARY KEY constraints.**
A: PRIMARY KEY uniquely identifies each row and cannot be NULL; a table can have only one. UNIQUE also ensures uniqueness but allows NULL values and a table can have multiple UNIQUE constraints.

**Q: Why use foreign keys instead of just storing related data together?**
A: Foreign keys maintain referential integrity, prevent orphaned records, enable efficient updates, support normalization, and provide clear relationship documentation. They enforce data consistency at the database level.

---

## Submission Checklist

### Files to Include in ZIP Folder:

- [ ] **PDF Document** containing:
  - Part 1: Introduction (Business description, operations, business rules)
  - Part 2: Initial ERD with entities and attributes
  - Part 3: Complete normalization (UNF → 1NF → 2NF → 3NF)
  - Part 4: Data dictionary and final ERD
  - Part 5: CREATE and INSERT statements with screenshots
  - Part 6: All 10 queries with screenshots of results
  - Part 7: Critical evaluation
  - Part 8: Properly formatted document
  - Part 9: Dump file creation and DROP statements with screenshots
  
- [ ] **Dump File**: `sajiloyatra_db.dmp`

- [ ] **Export Log**: `sajiloyatra_export.log` (optional but recommended)

### Naming Convention:
```
LondonMetID StudentFullName.zip
Example: 2404567 Kushal Sharma.zip
```

### Final Verification:
- [ ] All screenshots are clear and readable
- [ ] SQL statements are properly formatted
- [ ] All queries execute successfully
- [ ] Dump file is created and verified
- [ ] Tables are dropped in correct order
- [ ] PDF is professionally formatted
- [ ] File naming follows guidelines
- [ ] Submission before 09:00 PM deadline

---

## Conclusion

This comprehensive database solution for SajiloYatra demonstrates:

1. **Complete Database Design**: From conceptual modeling through normalization to physical implementation
2. **Referential Integrity**: Proper use of primary and foreign keys maintaining data consistency
3. **Normalized Structure**: All tables in 3NF eliminating redundancy and anomalies
4. **Practical Queries**: Both information and transaction queries supporting business operations
5. **Professional Documentation**: Clear explanation of design decisions and implementation details

The database effectively supports SajiloYatra's intercity travel operations including passenger management, trip scheduling, booking processing, ticketing, and payment tracking across Nepal's major cities.

**Total Tables: 9** (exceeds minimum requirement of 8)
**Total Test Data: 7+ rows per table** (meets requirement)
**All Requirements: Fulfilled**

---

## References and Resources

1. Oracle Database SQL Language Reference 12c
2. Date, C.J. "An Introduction to Database Systems" (8th Edition)
3. Elmasri, R. & Navathe, S.B. "Fundamentals of Database Systems"
4. Oracle SQL*Plus User's Guide and Reference
5. London Metropolitan University CC5051 Course Materials

---

**END OF COURSEWORK**

---

**Note for Students:**
- Review all SQL statements in Oracle SQL*Plus before submission
- Ensure all screenshots show both command and output
- Test all queries with your data
- Verify dump file can be imported successfully
- Prepare thoroughly for viva voce examination
- Maintain academic integrity throughout the coursework

**Good luck with your submission and viva!