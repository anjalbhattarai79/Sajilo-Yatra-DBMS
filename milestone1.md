# SajiloYatra — Milestone 1

## Part 1: Business Introduction and Operations

**Business name:** SajiloYatra — intercity travel service (Nepal)

**Founder:** Mr. Kiran Thapa (case study)

**Mission:** Provide seamless, reliable intercity transport across major Nepalese cities with online booking, centralized operations and customer-centric service.

### Core operations (summary)
- Route management: predefined routes with origin, destination, distance and estimated duration.
- Trip scheduling: multiple trips per route; each trip has date, departure/arrival times and assigned bus.
- Fleet management: buses with seating capacity, types and availability status (Available, Maintenance, Unavailable).
- Staff assignment: drivers and conductors assigned to buses/trips; staff have roles and contact details.
- Booking & ticketing: passengers make bookings selecting class (Regular / Premium / VIP); confirmed bookings generate tickets with fare and issue date.
- Payment processing: payments linked to tickets; records include amount, date and method.
- Passenger management: passengers stored once and referenced by bookings.

### Business rules (concise)
- BR1: Each route has unique Route_ID; connects exactly two locations; multiple trips per route; at least one bus assigned.
- BR2: Each trip belongs to exactly one route and one bus; has unique Trip_ID and records trip date/time.
- BR3: Each bus has unique Bus_ID and registration; capacity > 0; status tracked.
- BR4: Staff have unique Staff_ID; role is Driver or Conductor; multiple staff assigned to a bus.
- BR5: Passengers have unique Passenger_ID and contact info; can make multiple bookings.
- BR6: Each booking links a passenger to a trip; includes class, date and status; confirmed booking → one ticket.
- BR7: Tickets have unique Ticket_ID and link to one booking; record fare and issue date.
- BR8: Payments have unique Payment_ID and link to one ticket; amount must match fare; method recorded.
- BR9: Referential integrity: deleting a route cascades to its trips; deleting a trip cascades to bookings; passenger and staff records retained for history.
- BR10: Constraints: arrival > departure; booking date ≤ trip date; payment date ≥ ticket issue date; capacities and fares positive.

## Part 2: Initial ERD — Entities & Attributes

Below are the identified entities and primary attributes for Milestone 1 (initial ERD / conceptual model).

1. PASSENGER
   - Passenger_ID (PK)
   - Passenger_Name
   - Phone_Number
   - Email_Address
   - Address

2. ROUTE
   - Route_ID (PK)
   - Origin
   - Destination
   - Distance_KM
   - Estimated_Duration

3. BUS
   - Bus_ID (PK)
   - Bus_Registration_Number
   - Capacity
   - Bus_Type
   - Availability_Status

4. TRIP
   - Trip_ID (PK)
   - Route_ID (FK)
   - Bus_ID (FK)
   - Trip_Date
   - Departure_Time
   - Arrival_Time

5. STAFF
   - Staff_ID (PK)
   - Staff_Name
   - Role (Driver / Conductor)
   - Phone_Number
   - Hire_Date

6. BOOKING
   - Booking_ID (PK)
   - Passenger_ID (FK)
   - Trip_ID (FK)
   - Booking_Date
   - Booking_Class (Regular / Premium / VIP)
   - Booking_Status (Confirmed / Cancelled / Pending)

7. TICKET
   - Ticket_ID (PK)
   - Booking_ID (FK, unique)
   - Fare_Amount
   - Issue_Date

8. PAYMENT
   - Payment_ID (PK)
   - Ticket_ID (FK, unique)
   - Payment_Amount
   - Payment_Date
   - Payment_Method

9. BUS_STAFF_ASSIGNMENT
   - Assignment_ID (PK)
   - Bus_ID (FK)
   - Staff_ID (FK)
   - Assignment_Date

### Relationships (summary)
- PASSENGER 1:M BOOKING
- TRIP 1:M BOOKING
- BOOKING 1:1 TICKET
- TICKET 1:1 PAYMENT (payment optional until paid)
- ROUTE 1:M TRIP
- BUS 1:M TRIP
- BUS M:N STAFF via BUS_STAFF_ASSIGNMENT

## Files created for Milestone 1
- `milestone1.md` (this file) — narrative for Part 1 and Part 2
- `milestone1_erd.svg` — visual ERD (open with any browser/viewer)

## Next steps
- I will finalize the ERD visual and mark drafting complete after your review. If you want, I can also produce the SQL `CREATE TABLE` script and sample INSERTs for milestone submission.


---
*Prepared for CC5051 Milestone 1 — SajiloYatra*