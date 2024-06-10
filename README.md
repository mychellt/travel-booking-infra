# Docker Compose Configuration for Travel Booking Services

This `docker-compose.yml` file sets up the necessary services for the travel booking application, including separate PostgreSQL databases for hotel reservations, car rentals, travel bookings, flight reservations, and a RabbitMQ message broker. Each service runs in its own container with specified environment variables and ports.

## Services

### hotel-reservation-db

- **Image**: postgres:16-alpine
- **Ports**: 5432:5432
- **Environment Variables**:
  - `POSTGRES_DB`: hotel_reservation_db
  - `POSTGRES_USER`: `${DB_USER}`
  - `POSTGRES_PASSWORD`: `${DB_PASS}`
- **Volumes**:
  - `hotel-reservation-db-data:/var/lib/postgresql/data`

### car-rental-db

- **Image**: postgres:16-alpine
- **Ports**: 5433:5432
- **Environment Variables**:
  - `POSTGRES_DB`: car_rental_db
  - `POSTGRES_USER`: `${DB_USER}`
  - `POSTGRES_PASSWORD`: `${DB_PASS}`
- **Volumes**:
  - `car-rental-db-data:/var/lib/postgresql/data`

### travel-booking-db

- **Image**: postgres:16-alpine
- **Ports**: 5434:5432
- **Environment Variables**:
  - `POSTGRES_DB`: travel_booking_db
  - `POSTGRES_USER`: `${DB_USER}`
  - `POSTGRES_PASSWORD`: `${DB_PASS}`
- **Volumes**:
  - `travel-booking-db-data:/var/lib/postgresql/data`

### flight-reservation-db

- **Image**: postgres:16-alpine
- **Ports**: 5435:5432
- **Environment Variables**:
  - `POSTGRES_DB`: flight_reservation_db
  - `POSTGRES_USER`: `${DB_USER}`
  - `POSTGRES_PASSWORD`: `${DB_PASS}`
- **Volumes**:
  - `flight-reservation-db-data:/var/lib/postgresql/data`

### mq

- **Image**: rabbitmq:3-management-alpine
- **Ports**: 
  - 5672:5672 (AMQP port)
  - 15672:15672 (Management UI)
- **Environment Variables**:
  - `RABBITMQ_DEFAULT_USER`: `${RABBITMQ_DEFAULT_USER}`
  - `RABBITMQ_DEFAULT_PASS`: `${RABBITMQ_DEFAULT_PASS}`
- **Volumes**:
  - `mq-data:/var/lib/rabbitmq`

## Volumes

- `hotel-reservation-db-data`: Persistent storage for the hotel reservation database.
- `car-rental-db-data`: Persistent storage for the car rental database.
- `flight-reservation-db-data`: Persistent storage for the flight reservation database.
- `travel-booking-db-data`: Persistent storage for the travel booking database.
- `mq-data`: Persistent storage for RabbitMQ data.

## Environment Variables

Create a `.env` file in the root directory and define the following variables:

```dotenv
DB_USER=postgres
DB_PASS=postgres
RABBITMQ_DEFAULT_USER=admin
RABBITMQ_DEFAULT_PASS=admin
