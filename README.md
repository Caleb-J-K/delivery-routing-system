# Package Routing and Delivery Management System

A Python application that simulates package delivery operations using custom data structures and a nearest-neighbor routing algorithm. The system manages package constraints, assigns deliveries to trucks, calculates mileage, and provides package status information for any requested time.

This project was built using the Python standard library and emphasizes object-oriented design, data structures, algorithmic problem solving, and automated testing.

## Features

- Loads package, address, and distance data from CSV files
- Stores and retrieves packages using a custom hash table
- Plans delivery routes using a nearest-neighbor algorithm
- Handles package-specific delivery constraints
- Tracks truck locations, mileage, and delivery times
- Reports package status at user-specified times
- Includes 50 automated tests covering core application behavior

## Technologies and Concepts

- Python
- Object-Oriented Programming
- Data Structures and Algorithms
- Custom Hash Table
- Nearest-Neighbor Routing
- CSV Data Processing
- `datetime`
- `unittest`
- Git

## Project Structure

```text
delivery-routing-system/
├── data/
│   ├── distance_file.csv
│   └── package_file.csv
├── src/
│   ├── distance_table.py
│   ├── hash_table.py
│   ├── package.py
│   └── truck.py
├── tests/
│   ├── test_distance_table.py
│   ├── test_hash_table.py
│   ├── test_package.py
│   └── test_truck.py
├── main.py
├── .gitignore
└── README.md
```

## How It Works

The application loads package and distance information from CSV files and stores package records in a custom hash table.

Packages are assigned to delivery trucks according to delivery deadlines and package-specific constraints. Each truck begins at the delivery hub and selects its next destination using a nearest-neighbor approach based on the shortest available distance.

As deliveries are completed, the application updates package delivery times, truck locations, and total mileage. Package status can then be determined for a requested point in time.

## Package Constraints

The routing process accounts for several delivery requirements, including:

- Delivery deadlines
- Truck capacity
- Delayed package arrivals
- Packages restricted to a specific truck
- Packages that must be delivered together
- Address corrections that take effect during the delivery day

These constraints are handled during package assignment and delivery simulation so that routing decisions reflect the requirements associated with each package.

## Custom Hash Table

Package data is stored in a custom hash table implemented using separate chaining for collision handling.

The hash table supports:

- Insertion
- Lookup
- Updating existing records
- Removal
- Collision handling through separate chaining

Under normal conditions, insertion and lookup have an average time complexity of **O(1)**. In the worst case, when many keys collide into the same bucket, operations can approach **O(n)**.

Implementing the hash table from scratch provided direct experience with hashing, collision resolution, and the tradeoffs involved in data structure design.

## Routing Algorithm

The delivery simulation uses a **nearest-neighbor heuristic** to select the next package destination.

At each step:

1. Identify the packages that remain on the truck.
2. Calculate the distance from the truck's current location to each available destination.
3. Select the closest destination.
4. Travel to that location and deliver the package.
5. Update the truck's current location, time, mileage, and package status.
6. Repeat until all packages assigned to the truck have been delivered.

Nearest neighbor is straightforward and efficient for a relatively small delivery dataset, although it does not guarantee a globally optimal route.

### Complexity

For a truck carrying `n` packages, the algorithm may compare the current location against each remaining destination during every routing step.

This results in approximately:

```text
n + (n - 1) + (n - 2) + ... + 1
```

distance comparisons, giving the routing process a worst-case time complexity of approximately **O(n²)**.

The additional working space required by the routing logic is relatively small compared with the package and distance data already stored by the application.

## Distance Table Design

Distances between delivery locations are loaded from the provided CSV data into a distance table.

Because the distance between two locations is symmetric:

```text
distance(A, B) = distance(B, A)
```

the application can retrieve a distance regardless of which side of the source data contains the value.

This avoids duplicating distance information while still allowing the routing algorithm to request distances between any two known locations.

## Package Status Tracking

Each package maintains information used to determine its delivery state, including:

- Departure time
- Delivery time
- Assigned truck

Using these values, the application can determine whether a package was:

- At the hub
- En route
- Delivered

at a particular time during the simulated delivery day.

This allows the program to report historical package status rather than only displaying the final delivery state.

## Running the Application

### Requirements

- Python 3
- No third-party packages are required

Clone the repository:

```bash
git clone https://github.com/Caleb-J-K/delivery-routing-system.git
cd delivery-routing-system
```

Run the application:

```bash
python main.py
```

Depending on your system, you may need to use:

```bash
python3 main.py
```

## Running the Tests

The project includes **50 automated tests** covering core functionality and edge cases across the package, hash table, distance table, truck, and delivery behavior.

Run the complete test suite with:

```bash
python -m unittest discover
```

The tests are designed to verify areas including:

- Package creation and state
- Hash table insertion, lookup, updates, removal, and collision handling
- Distance-table loading and distance retrieval
- Truck initialization and package management
- Capacity restrictions
- Truck movement and time tracking
- Delivery-related behavior
- Error handling and edge cases

## Design Decisions

### Custom Hash Table

A custom hash table was used rather than Python's built-in dictionary to demonstrate the implementation and behavior of a fundamental data structure, including hashing and collision resolution.

### Object-Oriented Design

Packages, trucks, the hash table, and distance data are represented by separate components with distinct responsibilities. This keeps delivery logic organized and makes individual components easier to test and maintain.

### Standard Library Only

The application uses Python's standard library rather than external dependencies. This keeps setup simple and allows the project to focus on the underlying data structures, routing logic, and application design.

### Automated Testing

Automated tests are used to verify individual components and delivery behavior. The test suite grew alongside the project and currently contains 50 tests, providing a repeatable way to validate changes and catch regressions.

## Future Improvements

Potential future enhancements include:

- Compare the nearest-neighbor heuristic with alternative route optimization approaches
- Add persistent package tracking history
- Add a graphical or web-based user interface
- Expand input validation and error reporting
- Add additional route and integration testing
- Provide route visualization and delivery statistics

## What I Learned

This project provided hands-on experience applying computer science concepts in a complete application rather than implementing them only as isolated exercises.

Key areas included:

- Designing and implementing a hash table with collision handling
- Applying algorithm analysis to routing decisions
- Modeling state and behavior with object-oriented programming
- Working with structured CSV data
- Managing time-dependent package and truck state
- Translating delivery constraints into application logic
- Writing automated tests for individual components and application behavior
- Organizing a Python project into reusable modules

The project also reinforced the importance of balancing algorithmic efficiency, maintainability, correctness, and practical constraints when designing software.
