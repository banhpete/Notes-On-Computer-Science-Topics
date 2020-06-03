# PB-Notes-On-Computer-Science-Topics
My notes while studying the following Computer Science Topics:
- [Recursion](#recursion)

## Recursion
### What is Recursion
Recursion, by definition, is the repetition of a, well, repetitive procedure. In the context of programming and computer science, it's the repetition of some function, by having the function call itself over and over, to solve some problem by breaking it down to smaller problems.

For example, below is an example of solving the problem of finding a the n fibbonacci number in the fibbonacci sequence. See how the function is essentially calling itself up again during the return.
```
int fib(int n) {
   // Base case
   if (n == 0 || n == 1) return n;
 
   // Recursive step
   return fib(n-1) + fib(n-2);
}
```

### When do we use Recursion
So when do we want to use recursion? Initially, to someone who is new, recursion may not seem neccessary at all, the thought may be that anything that can be solved using recursion can just be done iteratively with some sort of loop since, as we mentioned above, it's used for problems that requires reptition. This is far from the truth. While it is true that there are recursions solutions which could easily be solved with loops, there are situations where loops would not work at all and recursion would be the best answer.

Now what are these situations? Essentially, any solution where you have one number, or you start at some point, and you need to branch off and check if there is a valid answer and if not go back to an original point and branch off again, essentially when you know that your answer requires checking serveral different values, and these values are all connected to one value. Take for example the Flood Fill function, which can be seen happening in a game like Minesweeper where you can click on an empty square and it uncovers surrounding empty squares up until it reaches a non-empty square. What's happening here is that the first square will be uncovered, and then you have to check the surrounding squares in all directions, if there are any empty squares surrounding it, then you uncover those squares and check the square surrounding those, and then so on and so on until you reach a non-empty square. Based on the example above, you can see that it would be difficult to set up a function with a loop because there several loops occuring at different points, and you don't know how many will need to occur. So to summarize, recursion would be best when:
 - Your solution requires some sort of branching from a singular point
 - The solutions seems like it requires several loops
 - You know when you would like to stop a loop/repitive action but you don't when you will get there.
 
### How do we write recursion?
This is the trickest part, recursion is difficult and requires practice! 

First thing to consider is the base case, essentailly, at what point dp we want to stop the recusions. See for example the solution for the Fibonacci number, the base case is when n=0 or n=1, essentially, when the fibonacci sequence calls fib(0) and fib(1) stop calling fib! The base case is very important for recursion, otherwise, we just have endless recursion.

Next consider what you want to get out of this solution. If the situation calls for a list of all possible combinations, then we need an array returned, and this most likely will call for some global variable we can push to. If it just requires one value, our recursive function returns one value everytime.

Also consider how do we get to the base case, what will we do the data that we are following. Whatever we do, we will most likely have it mutate when we call the recursive function again, see the fibbonacci function as an example, each time we call it, we subtract 1 from n.
