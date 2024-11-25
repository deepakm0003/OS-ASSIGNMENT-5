        OS ASSIGNMENT 5 
                    SimpleThreader
                                         GROUP NO:- 40 
       Name :- Deepak Meena (2023188) , Milind Kumar (2023320)
Overview
The SimpleThreader Library is a lightweight C++ threading utility that provides simplified parallel execution of code using the pthread library. It supports both 1D and 2D range-based parallelism, enabling users to execute functions in parallel over a defined range of indices. This library is designed for applications that benefit from multi-threaded computation.

Features
Parallel For (1D):
Execute a function over a 1D range ([low, high)) in parallel, split across multiple threads.
Parallel For (2D):
Execute a function over a 2D range ([low1, high1) x [low2, high2)) in parallel, split across multiple threads.
Chunk Splitting:
Automatically splits the range into near-equal chunks for efficient load balancing.
Performance Measurement:
Measures and displays the execution time of the parallel operations.
Demonstration Framework:
Includes a wrapper for running user-defined demonstrations.

API Documentation
1. parallel_for (1D)
cpp
Copy code
void parallel_for(int low, int high, 
                  std::function<void(int)> &&lambda, 
                  int numThreads);

Parameters:
low and high: Define the range [low, high) over which the function will execute.
lambda: A lambda function of type std::function<void(int)> to be executed.
numThreads: Number of threads to use.
Example Usage:
cpp
Copy code
parallel_for(0, 100, [](int i) {
    std::cout << "Processing index: " << i << "\n";
}, 4);


2. parallel_for (2D)
cpp
Copy code
void parallel_for(int low1, int high1, 
                  int low2, int high2, 
                  std::function<void(int, int)> &&lambda, 
                  int numThreads);

Parameters:
low1, high1: Define the row range [low1, high1).
low2, high2: Define the column range [low2, high2).
lambda: A lambda function of type std::function<void(int, int)> to be executed.
numThreads: Number of threads to use.
Example Usage:
cpp
Copy code
parallel_for(0, 10, 0, 10, [](int i, int j) {
    std::cout << "Processing index: (" << i << ", " << j << ")\n";
}, 4);


3. demonstration
cpp
Copy code
void demonstration(std::function<void()> &&lambda);

Purpose:
A utility function for wrapping and executing a user-defined demonstration or initialization function.
Example Usage:
cpp
Copy code
demonstration([]() {
    std::cout << "Welcome to the demonstration!\n";
});


Code Structure
Key Components
ThreadArgs & ThreadArgs2D:
Structures used to store thread-specific arguments for 1D and 2D parallelism.
Thread Functions:
thread_func_1D: Executes a function over a 1D range.
thread_func_2D: Executes a function over a 2D range.
Chunk Calculation:
Automatically splits the range into chunks, ensuring fair distribution across threads.
Performance Measurement:
Uses std::chrono to calculate and display execution time.

Sample Program
Here's an example of how to use the SimpleThreader library:
cpp
Copy code
#include "simple_threader.h"

int user_main(int argc, char** argv) {
    // Example 1: 1D Parallel For
    parallel_for(0, 20, [](int i) {
        std::cout << "Index: " << i << "\n";
    }, 4);

    // Example 2: 2D Parallel For
    parallel_for(0, 10, 0, 5, [](int i, int j) {
        std::cout << "Processing (" << i << ", " << j << ")\n";
    }, 3);

    return 0;
}


Build and Run
Compilation
Use the following command to compile your program
Make
./vector 2 100
./matrix 4 1024
Or 
g++ -pthread -std=c++17 -o simple_threader_demo your_program.cpp

Running the Program
Execute the program with:
./simple_threader_demo


Output Example
For a 1D range [0, 10) split across 2 threads:
mathematica
Copy code
Thread <ID>: Processing range 0 to 4
Thread <ID>: Processing range 5 to 9
1D Parallel_for Execution Time: 5 ms

For a 2D range [0, 3) x [0, 3):
mathematica
Copy code
Thread <ID>: Processing rows 0 to 1
Thread <ID>: Processing rows 2 to 2
2D Parallel_for Execution Time: 7 ms



Contributions :- 

Deepak's Contribution: Deepak designed the core threading architecture, implementing the calculate_chunks() template function that dynamically distributes workload across threads. He developed the sophisticated chunk allocation algorithm that ensures even work distribution by calculating base chunk sizes and handling remainder elements, enabling efficient parallel processing for both 1D and 2D computational scenarios.


Milind's Contribution: Milind focused on the lambda-based execution framework, creating the thread_func_1D() and thread_func_2D() functions that enable flexible parallel processing. He implemented the performance measurement mechanism using std::chrono::high_resolution_clock, which allows tracking and reporting execution times, and added thread range visualization to provide insights into parallel task execution.





