#include <iostream>

using namespace std;

int main() {
    // Prompt the user for the length and width of the rectangle
    cout << "Enter the length of the rectangle: ";
    double length;
    cin >> length;

    cout << "Enter the width of the rectangle: ";
    double width;
    cin >> width;

    // Calculate the area and perimeter of the rectangle
    double area = length * width;
    double perimeter = 2 * (length + width);

    // Display the calculated values to the user
    cout << "The area of the rectangle is: " << area << endl;
    cout << "The perimeter of the rectangle is: " << perimeter << endl;

    return 0;
}
