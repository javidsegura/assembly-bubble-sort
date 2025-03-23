

# EFFICIENT BUBBLE SORT, ASSEMBLY IMPLEMENTATION

### Introduction
In this code I have decided to implement in assembly the traditional bubble sort algorithm, an introductory algorithm taught in most CS majors. This implementation is part of my course in computer architecture.

### Algorithm Explained
At each pass through the array (inner loop) you compare if the adjacent element is greater than the current element. If so, you swap the elements (for descending order, setting JP NC, NO_SWAP; for ascending order, setting JP C NO_SWAP), else you move on to the next element. At each iteration of the algorithm (outer loop) the greatest element bubbles up to the top. An efficient implementation of bubble sort requires the outer loop to iterate n-i-1, where n is the number of elements and i is the current outer loop iteration. Moreover, an efficient implementation requires to stop iteration (outer loop) if a pass did not perform any swap. The presented assembly implementation contains these optimizations.
![bubbleSort](https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif)

### Z80, Assembly language implementation
Instructions are set at the beginning of memory (in the area designated to ROM, specifically) –0x0000. We define macro-like constructs at the top of the program. These assisted significantly in the process of debugging, as a single change propagated all the way down the program (instead of manual replacing). 
The C register is always in charge of keeping track of the swap flag, A for arithmetic operations, B the inner loop counter and H for the outer loop counter. We use IX for indexing addressing mode through the array. 
Two subroutines are used, one for swapping and another for continuing to the next loop. The reason for the latter is that you want to make sure that you only increment the outer loop counter if you are going to iterate one more time. Otherwise, you may kept some misleading data in the registers at the last iteration. Inner loop and outer loop use JP NZ with respect to the zero flag from the prior instruction in order to determine if another iteration is needed. This essentially emulates a traditional for loop in other programming languages. The program halts at the end of the iterations, setting the CPU at rest state with the sorted values in memory). 

### Proof Of Functionality
First state of memory:
![image](https://github.com/user-attachments/assets/75d04409-b96e-4aaf-b228-1f04c0c7678b)
After executing the program:
![image](https://github.com/user-attachments/assets/a9ad6e03-a858-456d-88d3-28fbb34f921b)

where, 
| Hexadecimal | Decimal |
|------------|--------|
| 01         | 1      |
| 0A         | 10     |
| 1E         | 30     |
| 3C         | 60     |
| 63         | 99     |
