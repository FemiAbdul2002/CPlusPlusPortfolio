# C++ Rectangle Calculator with Database Storage

## Overview
This program calculates the area and perimeter of a rectangle based on user input. It now includes **database functionality** using a text file to store and retrieve previous calculations.

## Features
✅ Accepts user input for **length** and **width**  
✅ **Calculates** and **displays** the area and perimeter  
✅ **Stores calculations** in a text file (simulating a database)  
✅ **Retrieves and displays previous calculations** on startup  
✅ **Validates user input** to prevent errors  

## How It Works
1. When the program starts, it **retrieves previous calculations** from `rectangle_data.txt`.  
2. The user enters the **length and width** of the rectangle.  
3. The program **calculates** the area and perimeter.  
4. The results are **displayed and saved** in `rectangle_data.txt`.  
5. Next time the program runs, previous results are **retrieved and shown** before new input.  

## How to Run
1. **Compile the program**:  
   ```sh
   g++ rectangle_calculator.cpp -o rectangle_calculator

Run the program
./rectangle_calculator




#include <iostream>
#include <fstream>  // File handling for storing data
#include <iomanip>  // Formatting output

using namespace std;

// Function to calculate area
double calculateArea(double length, double width) {
    return length * width;
}

// Function to calculate perimeter
double calculatePerimeter(double length, double width) {
    return 2 * (length + width);
}

// Function to save calculations to a file
void saveToDatabase(double length, double width, double area, double perimeter) {
    ofstream file("rectangle_data.txt", ios::app); // Open in append mode
    if (file.is_open()) {
        file << fixed << setprecision(2) 
             << length << " " << width << " " << area << " " << perimeter << endl;
        file.close();
        cout << "Data saved successfully.\n";
    } else {
        cout << "Error: Unable to open file for writing.\n";
    }
}

// Function to retrieve and display previous calculations
void retrieveFromDatabase() {
    ifstream file("rectangle_data.txt");
    if (file.is_open()) {
        double length, width, area, perimeter;
        cout << "\nPrevious Calculations:\n";
        cout << "Length  Width  Area  Perimeter\n";
        cout << "--------------------------------\n";
        while (file >> length >> width >> area >> perimeter) {
            cout << fixed << setprecision(2) 
                 << length << "   " << width << "   " << area << "   " << perimeter << endl;
        }
        file.close();
    } else {
        cout << "No previous data found.\n";
    }
}

int main() {
    double length, width, area, perimeter;
    
    // Retrieve previous calculations
    retrieveFromDatabase();

    // Get user input
    cout << "\nEnter the length of the rectangle: ";
    cin >> length;
    cout << "Enter the width of the rectangle: ";
    cin >> width;

    // Validate input
    if (length <= 0 || width <= 0) {
        cout << "Error: Length and width must be positive numbers.\n";
        return 1; // Exit program with error code
    }

    // Perform calculations
    area = calculateArea(length, width);
    perimeter = calculatePerimeter(length, width);

    // Display results
    cout << "The area of the rectangle is: " << area << endl;
    cout << "The perimeter of the rectangle is: " << perimeter << endl;

    // Save to file (simulating database)
    saveToDatabase(length, width, area, perimeter);

    return 0;
}
