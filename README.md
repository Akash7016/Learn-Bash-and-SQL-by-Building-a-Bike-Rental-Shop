# Bike Rental Shop

This repository contains a Bash script to manage a bike rental shop. The script interacts with a PostgreSQL database to allow users to rent and return bikes.

## Prerequisites

- PostgreSQL
- Bash

## Getting Started

1. **Clone the repository**:
    ```sh
    git clone https://github.com/yourusername/bike-rental-shop.git
    cd bike-rental-shop
    ```

2. **Set up the database**:
    - Ensure PostgreSQL is installed and running on your machine.
    - Create a database named `bikes` and set up the necessary tables.
    
    ```sql
    CREATE DATABASE bikes;

    \c bikes

    CREATE TABLE bikes (
      bike_id SERIAL PRIMARY KEY,
      type VARCHAR(50),
      size VARCHAR(50),
      available BOOLEAN DEFAULT TRUE
    );

    CREATE TABLE customers (
      customer_id SERIAL PRIMARY KEY,
      name VARCHAR(50),
      phone VARCHAR(20) UNIQUE
    );

    CREATE TABLE rentals (
      rental_id SERIAL PRIMARY KEY,
      customer_id INT REFERENCES customers(customer_id),
      bike_id INT REFERENCES bikes(bike_id),
      date_rented TIMESTAMP DEFAULT NOW(),
      date_returned TIMESTAMP
    );
    ```

3. **Populate the database with sample data** (optional):
    ```sql
    INSERT INTO bikes(type, size) VALUES ('Mountain', '26'), ('Road', '28'), ('Hybrid', '24');
    ```

4. **Run the script**:
    ```sh
    ./bike_rental.sh
    ```

## Script Functionality

### Main Menu
- **Rent a bike**: Displays available bikes and allows users to rent one.
- **Return a bike**: Allows users to return a bike they have rented.
- **Exit**: Exits the application.

### Renting a Bike
1. Displays a list of available bikes.
2. Prompts for the bike ID to rent.
3. Asks for the user's phone number to check if they are an existing customer.
4. If the user is a new customer, prompts for their name and adds them to the database.
5. Records the rental in the database and updates the bike's availability.

### Returning a Bike
1. Prompts for the user's phone number to identify them.
2. Displays the bikes currently rented by the user.
3. Prompts for the bike ID to return.
4. Updates the rental record with the return date and changes the bike's availability.

## Script Structure

- **MAIN_MENU**: Displays the main menu and handles user input.
- **RENT_MENU**: Manages the bike renting process.
- **RETURN_MENU**: Manages the bike returning process.
- **EXIT**: Exits the application.

