# Multi-Threading
/* Sanyerlis Camacaro- CSC275 - Sancamac@uat.edu Assignment: Multi-threading.
This code demonstrates how to:
Clearly use true multithreading.
Over comment all your code for the future you in your own words.
Your program should do something, in addition, to clearly demonstrating Multithreading.
You must have a good UX and keep the user over-informed of what is happening.

This program:

Defines two functions, sumEven and sumOdd, which calculate the sum of even and odd numbers 
in a given range, respectively.
Locks console output using a mutex to prevent overlapping text.
Takes user input for the start and end of the range.
Creates two threads, one for each function, and starts them.
Joins the threads to wait for their completion before exiting the program.
This example satisfies the given expectations: it uses true multithreading, 
is thoroughly commented, does something (summing even and odd numbers), 
and keeps the user informed of the process.
*/

#include <iostream> // includes input and out as the standard library.
#include <thread> // includes multithreading.
#include <mutex> // allows multiple program thread can take turns sharing the same resource, such as access to a file.
#include <chrono> // it also works as namespace.

using namespace std;// means using standard namespace and that I dont have to type std:: in front of each line.


// Mutex for synchronizing output to the console
mutex mtx;


// Function to sum even numbers in a given range
void sumEven(int start, int end) {

    long long sum = 0;

    for (int i = start; i <= end; i++) {

        if (i % 2 == 0) {

            sum += i;

        }

    }



    // Lock the console output
    unique_lock<mutex> lock(mtx);

    cout << "Sum of even numbers from " << start << " to " << end << " is: " << sum << endl;

    lock.unlock();

}


// Function to sum odd numbers in a given range
void sumOdd(int start, int end) {

    long long sum = 0;

    for (int i = start; i <= end; i++) {

        if (i % 2 == 1) {

            sum += i;

        }

    }


    // Lock the console output
    unique_lock<mutex> lock(mtx);

    cout << "Sum of odd numbers from " << start << " to " << end << " is: " << sum << endl;

    lock.unlock();

}

// Starts program
int main() {

    int start, end;


    // Get user input
    cout << "\nWelcome to Multi-threading Demo Assignment!\n" << endl;

    cout << "\nThis program demonstrates the creation, execution, and management of multiple threads.\n" << endl;

    cout << "It calculates the sum of all even and odd numbers in a given range separately using two threads." << endl;

    cout << "\nEnjoy the demo!\n" << endl;

    cout << "Enter the start of the range: ";

    cin >> start;

    cout << "Enter the end of the range: ";

    cin >> end;


    // Create two threads
    thread evenThread(sumEven, start, end);

    thread oddThread(sumOdd, start, end);

    cout << "Calculating the sum of even and odd numbers in the given range...\n";


    // Join the threads
    evenThread.join();

    oddThread.join();

    cout << "\nDone!\n";

    return 0;

}

