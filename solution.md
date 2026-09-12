# Laboratory Work 1: ERD Diagram for International Airport System

**Course Name:** Databases  
**Student:** Ернұрқызы Ақнұр  

---



1. **Airports**: `airport_id` (PK), `airport_name`, `country`, `state`, `city`, `created_at`, `updated_at`.
2. **Airlines**: `airline_id` (PK), `airline_code`, `name`, `country`, `created_at`, `updated_at`.
3. **Flights**: `flight_id` (PK), `departing_gate`, `arriving_gate`, `scheduled_departure_time`, `scheduled_arrival_time`, `actual_departure_time`, `actual_arrival_time`, `airline_id` (FK), `departure_airport_id` (FK), `arrival_airport_id` (FK), `created_at`, `updated_at`.
4. **Passengers**: `passenger_id` (PK), `first_name`, `last_name`, `gender`, `date_of_birth`, `country_of_citizenship`, `country_of_residence`, `passport_number`, `created_at`, `updated_at`.
5. **Bookings**: `booking_id` (PK), `flight_id` (FK), `passenger_id` (FK), `status`, `booking_platform`, `ticket_price`, `created_at`, `updated_at`.
6. **Booking_Changes**: `change_id` (PK), `booking_id` (FK), `change_description`, `created_at`, `updated_at`.
7. **Boarding_Passes**: `boarding_pass_id` (PK), `booking_id` (FK), `seat`, `boarding_time`, `created_at`, `updated_at`.
8. **Baggage**: `baggage_id` (PK), `booking_id` (FK), `weight_in_kg`, `created_at`, `updated_at`.
9. **Baggage_Checks**: `baggage_checking_id` (PK), `booking_id` (FK), `passenger_id` (FK), `check_result`, `created_at`, `updated_at`.
10. **Security_Checks**: `security_check_id` (PK), `passenger_id` (FK), `check_result`, `created_at`, `updated_at`.

---

## 2. Relationships & Cardinality Constraints

* **Airlines — Flights**: 1:N (One airline operates many flights).
* **Airports — Flights**: 1:N (One airport serves as departure/arrival for many flights).
* **Passengers — Bookings**: 1:N (One passenger can create multiple bookings).
* **Flights — Bookings**: 1:N (One flight contains many bookings).
* **Bookings — Booking_Changes**: 1:N (One booking can have multiple change records).
* **Bookings — Boarding_Passes**: 1:1 (Each booking generates one boarding pass).
* **Bookings — Baggage**: 1:N (One booking can include multiple baggage items).
* **Bookings / Passengers — Baggage_Checks**: 1:N.
* **Passengers — Security_Checks**: 1:N (A passenger undergoes security checks).

---

## 3. Entity-Relationship Diagram (ERD)

```mermaid
erDiagram
    AIRPORTS ||--o{ FLIGHTS : "departs/arrives"
    AIRLINES ||--o{ FLIGHTS : "operates"
    FLIGHTS ||--o{ BOOKINGS : "has"
    PASSENGERS ||--o{ BOOKINGS : "makes"
    BOOKINGS ||--o{ BOOKING_CHANGES : "tracks"
    BOOKINGS ||--|| BOARDING_PASSES : "generates"
    BOOKINGS ||--o{ BAGGAGE : "includes"
    BOOKINGS ||--o{ BAGGAGE_CHECKS : "checked_under"
    PASSENGERS ||--o{ BAGGAGE_CHECKS : "owns"
    PASSENGERS ||--o{ SECURITY_CHECKS : "undergoes"

    AIRPORTS {
        int airport_id PK
        string airport_name
        string country
        string state
        string city
        timestamp created_at
        timestamp updated_at
    }

    AIRLINES {
        int airline_id PK
        string airline_code
        string name
        string country
        timestamp created_at
        timestamp updated_at
    }

    FLIGHTS {
        int flight_id PK
        int airline_id FK
        int departure_airport_id FK
        int arrival_airport_id FK
        string departing_gate
        string arriving_gate
        timestamp scheduled_departure_time
        timestamp scheduled_arrival_time
        timestamp actual_departure_time
        timestamp actual_arrival_time
        timestamp created_at
        timestamp updated_at
    }

    PASSENGERS {
        int passenger_id PK
        string first_name
        string last_name
        string gender
        date date_of_birth
        string country_of_citizenship
        string country_of_residence
        string passport_number
        timestamp created_at
        timestamp updated_at
    }

    BOOKINGS {
        int booking_id PK
        int flight_id FK
        int passenger_id FK
        string status
        string booking_platform
        decimal ticket_price
        timestamp created_at
        timestamp updated_at
    }

    BOOKING_CHANGES {
        int change_id PK
        int booking_id FK
        string change_description
        timestamp created_at
        timestamp updated_at
    }

    BOARDING_PASSES {
        int boarding_pass_id PK
        int booking_id FK
        string seat
        timestamp boarding_time
        timestamp created_at
        timestamp updated_at
    }

    BAGGAGE {
        int baggage_id PK
        int booking_id FK
        decimal weight_in_kg
        timestamp created_at
        timestamp updated_at
    }

    BAGGAGE_CHECKS {
        int baggage_checking_id PK
        int booking_id FK
        int passenger_id FK
        string check_result
        timestamp created_at
        timestamp updated_at
    }

    SECURITY_CHECKS {
        int security_check_id PK
        int passenger_id FK
        string check_result
        timestamp created_at
        timestamp updated_at
    }