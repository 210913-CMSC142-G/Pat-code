# Integer Knapsack NP - Complete
>The following content is how the author understood the Integer Knapsack Problem. It is by no means claiming to be the formal definition of the Integer Knapsack Problem.

**The Integer Knapsack Problem** is a problem in combinatorial optimization: You are given a set of items, each with a weight and a value. You must determine the number of each item to include in a 'knapsack' so that the total weight is less than or equal to the maximum capacity of the 'knapsack' and the total value is as large as possible.

**Input:**
* N types of items; Each with a 'value' and 'weight'.
* Knapsack of Capacity C.

**Goal:**
* Choose items to pack into the knapsack to maximize the value.

## Integer Knapsack VS. Fractional Knapsack

In Integer Knapsack, you must either take the item, or not at all. On the other hand, in Fractional Knapsack, you can 'fraction' the objects and take those fractions (i.e. Value/Weight = ValuePerOneUnitOfWeight).

>(Note that the Fractional Knapsack Problem is not NP-Complete and is only mentioned for comparison).

**The Integer Knapsack Problem can be further divided into three more variants:**
* **The 0/1 Knapsack Problem:** Where you can only choose the item once.
* **The Bounded Knapsack Problem:** Where there is a 'bound' to the quantity of the item. (i.e. There are only 3 pcs of item A).
* **The Unbounded Knapsack Problem:** Where there is unlimited quantity for all objects. 

For this document, we shall be focusing on the Unbounded Knapsack Problem, we are going to be looking at a bottom-up approach from the Dynamic Programming Algorithm to solve this problem.


## Snippet from Dynamic Programming Code Solution for the Unbounded Knapsack Problem:

	//Declaration of the array
        int dp[] = new int[Capacity + 1];
        
        //This is the part that fills the db
        for(int i = 0; i <= Capacity; i++){
            for(int j = 0; j < n; j++){
                if(wt[j] <= i){
                    dp[i] = maximum(dp[i], dp[i - wt[j]] +
                                val[j]);
                }
            }
In this code, we first declare a new array named dp with size of Capacity + 1 to accommodate for the 0 value. After that we see the nested for loops used to fill the array. What the for loop does is iterate over all the items available for each capacity of the 'knapsack'  from 0 all the way to the maximum capacity. It checks if with this, we can achieve a greater value from the current one we have. 

For an example with the following inputs:
>int Capacity = 8;
        int val[] = {30, 80, 55, 65};
        int wt[] = {2, 7, 4, 3};

The first three iterations of the array would look like this:
|     |     |     |     |     |     |     |     |
|-----|-----|-----|-----|-----|-----|-----|-----|
|  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |
|  0  |  0  |  30  |  0  |  0  |  0  |  0  |  0  |
|  0  |  0  |  30  |  65  |  0  |  0  |  0  |  0  |

The final iteration of the array would look like this:
|     |     |     |     |     |     |     |     |
|-----|-----|-----|-----|-----|-----|-----|-----|
|  0  |  0  |  30  |  65  |  95  |  130  |  130  |  160  |

The maximum value we can achieve for this set of inputs is : 160

>This code has O(n x W) time complexity.


## Why is it NP-Complete?

**Reduction**
We can actually reduce known NP-Complete Problem Subset-Sum to Integer Knapsack. On that note, we can also reduce famous NP-Complete Problem, 3SAT to Subset-Sum. The reduction chain you could do would look like something like this:

   **3SAT => Subset-Sum =>Integer Knapsack**
   >Note that this is not a direct path and other problems woul most likely still be in between these three.
   >Check the following links for full solution to the reduction:
   >https://people.orie.cornell.edu/dpw/orie6300/Lectures/lec25.pdf
   >https://www.cc.gatech.edu/~rpeng/CS3510_F16/notes/Nov28knapsackNPC.pdf

**Pseudo-Polynomial**
The time complexity O(n x W) is actually not a polynomial but a ***pseudo-polynomial***. Meaning that it looks like it is polynomial, but it is actually exponential when viewed/re-written in binary (in number of bits needed to represent the value of the input).

Example:
When n = 4 = 100(in binary) = 3 bits is needed to represent it.
When n = 8 = 1000(in binary) = 4 bits is needed to represent it.
When n = 1,000,000,000,000 = 40 bits is needed to represent it. 

So O(n x W) is more accurately viewed by our machines as O(n x 2<sup>bits in W</sup>) which is exponential. 
>Note that n here is not changed to these format because n is not the **value** of the input, it is the **number** of input.

**Weakly NP-Complete**
Since the Integer Knapsack Problem is solved using a pseudo - polynomial time complexity algorithm, it is considered *weakly NP-Complete.* Other NP-Complete problems that fall under this category is Partition Problem and Subset-Sum Problem. 

## References

CMSC 451: Subset sum & knapsack - carnegie mellon school ... (n.d.). Retrieved December 11, 2021, from https://www.cs.cmu.edu/~ckingsf/bioinfo-lectures/subsetsum.pdf.

CS 3510 Design & Analysis of algorithms NP-completeness of ... (n.d.). Retrieved December 12, 2021, from https://www.cc.gatech.edu/~rpeng/CS3510_F16/notes/Nov28knapsackNPC.pdf.

Integer Knapsack problem - dynamic programming solutions. Sanfoundry. (2017, June 5). Retrieved December 10, 2021, from https://www.sanfoundry.com/dynamic-programming-solutions-integer-knapsack-problem/.

The Integer Knapsack problem, by Brian Dean - YouTube. (n.d.). Retrieved December 07, 2021, from https://www.youtube.com/watch?v=YTGSM5BLOxM.

NP-completeness - CPP. (n.d.). Retrieved December 12, 2021, from https://www.cpp.edu/~gsyoung/CS3310/CS3310Notes/NP-Completeness.pdf.

Pseudo-polynomial algorithms. GeeksforGeeks. (2021, August 22). Retrieved December 11, 2021, from https://www.geeksforgeeks.org/pseudo-polynomial-in-algorithms/.

Reductions - courses.engr.illinois.edu. (n.d.). Retrieved December 12, 2021, from https://courses.engr.illinois.edu/cs374/sp2016/notes/reductions.pdf.

Why is the Knapsack problem pseudo-polynomial? - youtube. (n.d.).
Retrieved December 07, 2021, from
https://www.youtube.com/watch?v=9oI7fg-MIpE.



