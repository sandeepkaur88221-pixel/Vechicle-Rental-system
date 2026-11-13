VEHICLE RENTAL SYSTEM
OOP Project in C++
1. Introduction
The Vehicle Rental System is a C++ project that helps manage vehicle rentals. Customers can view available vehicles, rent a vehicle, and return it.
This project uses Object-Oriented Programming concepts such as classes, objects, encapsulation, inheritance, and polymorphism.
2. Objectives
To manage vehicle details.
To display available vehicles.
To rent a vehicle.
To return a rented vehicle.
To calculate rental charges.
To understand OOP concepts using C++.
3. OOP Concepts Used
Class: A blueprint for creating objects.
Object: An instance of a class.
Encapsulation: Combines data and functions in one class.
Inheritance: Allows one class to use features of another class.
Polymorphism: Allows the same function interface to behave differently for different vehicle types.
Abstraction: Shows essential features while hiding implementation details.
4. C++ Source Code
The following is a simple, menu-driven project suitable for a college assignment.
#include <iostream>
#include <string>
using namespace std;

class Vehicle
{
protected:
    int id;
    string name;
    double rent;
    bool available;

public:
    Vehicle(int i, string n, double r)
    {
        id = i;
        name = n;
        rent = r;
        available = true;
    }

    virtual void display()
    {
        cout << id << "\t" << name << "\tRs. "
             << rent << "\t"
             << (available ? "Available" : "Rented")
             << endl;
    }

    int getId()
    {
        return id;
    }

    bool isAvailable()
    {
        return available;
    }

    void rentVehicle()
    {
        available = false;
    }

    void returnVehicle()
    {
        available = true;
    }

    double calculateRent(int days)
    {
        return rent * days;
    }

    virtual ~Vehicle() {}
};

class Car : public Vehicle
{
public:
    Car(int i, string n, double r)
        : Vehicle(i, n, r) {}

    void display() override
    {
        cout << id << "\tCar - " << name
             << "\tRs. " << rent
             << "\t" << (available ? "Available" : "Rented")
             << endl;
    }
};

class Bike : public Vehicle
{
public:
    Bike(int i, string n, double r)
        : Vehicle(i, n, r) {}

    void display() override
    {
        cout << id << "\tBike - " << name
             << "\tRs. " << rent
             << "\t" << (available ? "Available" : "Rented")
             << endl;
    }
};

int main()
{
    Vehicle* vehicles[4];

    vehicles[0] = new Car(1, "Swift", 2000);
    vehicles[1] = new Car(2, "i20", 1800);
    vehicles[2] = new Bike(3, "Honda", 500);
    vehicles[3] = new Bike(4, "Royal Enfield", 1000);

    int choice, id, days;
    bool found;

    do
    {
        cout << "\n===== VEHICLE RENTAL SYSTEM =====\n";
        cout << "1. Display Vehicles\n";
        cout << "2. Rent Vehicle\n";
        cout << "3. Return Vehicle\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
        case 1:
            cout << "\nID\tVehicle\t\tRent/Day\tStatus\n";

            for (int i = 0; i < 4; i++)
                vehicles[i]->display();

            break;

        case 2:
            cout << "Enter Vehicle ID: ";
            cin >> id;

            found = false;

            for (int i = 0; i < 4; i++)
            {
                if (vehicles[i]->getId() == id)
                {
                    found = true;

                    if (vehicles[i]->isAvailable())
                    {
                        cout << "Enter rental days: ";
                        cin >> days;

                        if (days <= 0)
                        {
                            cout << "Invalid number of days!\n";
                            break;
                        }

                        cout << "Total Rent: Rs. "
                             << vehicles[i]->calculateRent(days)
                             << endl;

                        vehicles[i]->rentVehicle();

                        cout << "Vehicle rented successfully!\n";
                    }
                    else
                    {
                        cout << "Vehicle is already rented!\n";
                    }

                    break;
                }
            }

            if (!found)
                cout << "Vehicle not found!\n";

            break;

        case 3:
            cout << "Enter Vehicle ID: ";
            cin >> id;

            found = false;

            for (int i = 0; i < 4; i++)
            {
                if (vehicles[i]->getId() == id)
                {
                    found = true;

                    if (!vehicles[i]->isAvailable())
                    {
                        vehicles[i]->returnVehicle();
                        cout << "Vehicle returned successfully!\n";
                    }
                    else
                    {
                        cout << "This vehicle was not rented.\n";
                    }

                    break;
                }
            }

            if (!found)
                cout << "Vehicle not found!\n";

            break;

        case 4:
            cout << "Thank you for using the system!\n";
            break;

        default:
            cout << "Invalid choice!\n";
        }

    } while (choice != 4);

    for (int i = 0; i < 4; i++)
        delete vehicles[i];

    return 0;
}
5. Sample Output
===== VEHICLE RENTAL SYSTEM =====
1. Display Vehicles
2. Rent Vehicle
3. Return Vehicle
4. Exit

Enter your choice: 1

ID    Vehicle          Rent/Day    Status
1     Car - Swift      Rs. 2000    Available
2     Car - i20        Rs. 1800    Available
3     Bike - Honda     Rs. 500     Available
4     Bike - Royal Enfield Rs. 1000 Available
Example: Renting a Vehicle
Enter your choice: 2
Enter Vehicle ID: 3
Enter rental days: 2

Total Rent: Rs. 1000
Vehicle rented successfully!
Example: Returning a Vehicle
Enter your choice: 3
Enter Vehicle ID: 3

Vehicle returned successfully!
6. How OOP Is Used in This Project
OOP Concept
Application
Class
Vehicle, Car, and Bike
Object
Individual cars and bikes
Encapsulation
Vehicle data and related functions are grouped in a class
Inheritance
Car and Bike inherit from Vehicle
Polymorphism
The display() function is overridden in derived classes
Abstraction
Users interact with the menu without needing to know the internal implementation
7. Advantages
Easy to use.
Displays vehicle availability.
Calculates rental charges automatically.
Prevents renting an already-rented vehicle.
Demonstrates important OOP concepts.
Can be extended with more features.
8. Limitations
Customer details are not stored.
Data is not saved permanently after the program closes.
The project does not include online payments.
Only four vehicles are available in this version.
9. Future Scope
The project can be improved by adding:
Customer registration and login.
Database connectivity.
More vehicle types.
Booking dates and times.
Online payment facilities.
Rental receipts and reports.
10. Conclusion
The Vehicle Rental System is a simple C++ project based on Object-Oriented Programming. It helps manage vehicle availability, rental charges, and vehicle returns. This project demonstrates how classes, objects, inheritance, encapsulation, abstraction, and polymorphism can be used to
