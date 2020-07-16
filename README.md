# PB-Notes-On-Computer-Science-Topics
My notes while studying the following Computer Science Topics:
- [Big O](#big-o)
- [Recursion](#recursion)
- [Sorting](#sorting)
- [Data Structures](#data-structures)

## Big O
Big O Notation is a way of describing time and space complexities of our codes/agorithms in terms of general mathematical functions.
-Space complexitiy is described in one of two formats, in place and out of place.
   - In place types do not depend on size of the input and the space it takes is predictable
   - Out of place is the opposite, it needs more space. I suppose we can think of it as it's out of place because it needs more space!
-The time complexity of a complicated can be determined by splitting it up and then multiplying them, think of the Merge Sort, which can be split into two different time complexities. One which is O(log(N)) and one which is O(N), this results in Merge Sort being O(N log(N))

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
So when do we want to use recursion? Initially, to someone who is new, recursion may not seem neccessary at all especially since recursion may use a lot of memory as you fill up the call stack. The thought may be that anything that can be solved using recursion can just be done iteratively with some sort of loop since, as we mentioned above, it's used for problems that requires reptition. This is far from the truth. While it is true that there are recursions solutions which could easily be solved with loops, there are situations where loops would not work at all and recursion would be the best answer.

Now what are these situations? Essentially, any solution where you have one number, or you start at some point, and you need to branch off and check if there is a valid answer and if not go back to an original point and branch off again, essentially when you know that your answer requires checking serveral different values, and these values are all connected to one value. Take for example the Flood Fill function, which can be seen happening in a game like Minesweeper where you can click on an empty square and it uncovers surrounding empty squares up until it reaches a non-empty square. What's happening here is that the first square will be uncovered, and then you have to check the surrounding squares in all directions, if there are any empty squares surrounding it, then you uncover those squares and check the square surrounding those, and then so on and so on until you reach a non-empty square. Based on the example above, you can see that it would be difficult to set up a function with a loop because there several loops occuring at different points, and you don't know how many will need to occur. So to summarize, recursion would be best when:
 - Your solution requires some sort of branching from a singular point
 - The solutions seems like it requires several loops
 - You know when you would like to stop a loop/repitive action but you don't when you will get there.

 
### How do we write recursion?
This is the trickest part, recursion is difficult and requires practice! 

First thing to consider is the base case, essentailly, at what point dp we want to stop the recusions. See for example the solution for the Fibonacci number, the base case is when n=0 or n=1, essentially, when the fibonacci sequence calls fib(0) and fib(1) stop calling fib! The base case is very important for recursion, otherwise, we just have endless recursion.

Next consider what you want to get out of this solution. If the situation calls for a list of all possible combinations, then we need an array returned, and this most likely will call for some global variable we can push to and what is a known as a recusrive helper function. If it just requires one value, our recursive function returns one value everytime.

Also consider how do we get to the base case, what will we do the data that we are following. Whatever we do, we will most likely have it mutate when we call the recursive function again, see the fibbonacci function as an example, each time we call it, we subtract 1 from n.

### Additional Notes on Recursion
- A recursive helper function is essentially a function within another function, why might we do this? To remove the concern for needing for a recursive function to hold onto infomation with parameters, the outer function can be used to hold onto information. These functions are helpful for when we need to return a list of combinations.

## Sorting
In regards to sorting algorithms, below are some notes:
### Insertion and Bubble
- There are stable sorts and and unstable sorts. Stable sorts keep the initial order of a collection after sorting by some other feature/attribute. This is important to consider especially when you are sorting by two different factors, otherwise, you may not get what you want.
- There are two types of sorting, distribution sorting and comparison sorting. The names are self-explanatory, essentially one will sort items in a group of other items, and the other compare items to other items for sorting.
- **Bubble Sort** is one of the least inefficient sorting algorithms but it's going to know about how it's done to give us content. Bubble sorts starts at one end and then compares the first pair of numbers, and swaps the numbers if the first number is greater than the second number. Then it moves to the second and third number and compares and swaps if necessary, and then so on and so on. This way, the largest number bubbles to the very end, and then we start all over again to have the second largest number bubble to the end.
- **Insertion Sort** is when you start at the beginning and then consider the second number and insert it in the right place (considering the two numbers), then move to the next number and insert where it makes sense, and so on and so on. **Bubble Sort and Insertion Sort are the same in terms of their time and space complexity being O(N^2) and O(1) respectively, and both are stable**.
### Divide and Conquer
- Quick Sort and Merge Sort are considered the divide and conquer sorts cause well.. they divide and conquer the collection! Essentially they break down whatever collection we have into multiple smaller pieces (through recursion) and then sort the smaller pieces.
-**Merge Sort** is the sort that first breaks the collection down through recursion in 1 element long, then they combine the elements such that there are several groups of 2, and those sort those, then they comebine again such that there is a group of 4 now, and that is sorted, and so on and so on. If there's an odd number, that's fine too, there can be groups of 3.
-**Quick Sort** is when we pick a pivot in the collection, partition the collection based on that pivot such that all elements lower is one side and all elements higher is on the other side. After this is done, we do it again on the two new sides we created! Partition based on pivot! How can we partition it? Pick a random pivot number, then go through the array to create two new arrays, one where it's larger than the pivot and one where it's smaller than pivot. Then we combine, the array with smaller elements, the pivot, and the array with larger elements together *BUT* only after doing the same thing with the other two elements.
-It's interesting to note that in terms of Big O Notation, merge sort is O(N log(N)) but Quick Sort is O(N^2), however both algorithms are actually considered to be really effective at sorting, how is this possible? Well, recall Big O Notation is only based on worst case scenario, but generally, on average, they're both O(average)(log(N)). Also consider the fact that Quick Sort uses less memory (O(log(N)), remember merge sorts creates an array for every element! Memory can affect the overall speed as well!
### Bucket and Radix Sorting
- Bucket and Radix sorting are distribution sorts as the main concept of the sort algorithim is sorting them into specific groups, rather than comparing to one another.
- For **Bucket Sorting**, you'll need to determine what buckets you have first, and then you sort your items into each bucket. With that in mind, we obivously need to determine what buckets we have, for a collection of numbers, determine the max and min of the numbers, determine the number of buckets we need (usually the square root of the total number of items) and then we can determine our bucket ranges. After this we can create separate arrays for each bucket, and then we can start looping through the array. Using what we know about our min, and bucket sizes (magnitude of their range) we take each item and sort them to their respective bucket. Once all items are sorted into each bucket we can sort each of them which will be faster since we're doing it at a smaller scale, and then we combine them.
- For **Radix Sorting**, it can almost be like layers of distribution sorting, where we sort by the radix of an item, also known as the base of an item. So when it comes to numbers, we're sorting by each base which means we can sort all items by their Least significant digit, then the next significant digit, and then the next significant digit. Now keep in mind, for radix sorting to work, it needs to be a stable sorting such that we don't lose the order of the numbers when we sort multiple times, otherwise if the sorting is not stable it defeats the purpose of the subsequent sorting. So to begin (when we're working with numbers), we need to create buckets, one for each possible digit, essentially we need 10 buckets, representing 0-9. Once we have our buckets, we loop through our collection of items, and sort them to their respective bucket based on their LSD, once we do that, we can combine all arrays and now they're sorted based on the LSD. Then we recreate the buckets, and loop through this new array and distribute them to their respective bucket based on the next significant digit, and then so on and so on.
- Now for these types of sorting methods, the data is prefered to be densed in the sense that we don't have a huge range. For examples if we were sorting 10 numbers and the minimum number was 3 and the maximum numbers was 1000, but all the other numbers were around 1-30, can you imagine how are buckets will look like? Most elements will fall in one bucket, and this really defeats the purpose of distribution sorting because you're not breaking it into smaller groups and sorting them.
### Binary Search
The Binary Search Algorithim is an algorithm for sorted arrays and only sorted arrays and it is extremely fast. Essentially when going through a collection of items that are sorted you start at the very middle of the collection and then you can decide which side of the collection will have the item you're looking for. Once you do, you discard the other side of the array and you look at the middle of the array you picked, is it the item you're look for? If yes, sweet! If no, then again decide which side of the collection you want and which side you'll discard. So this code will require you to repeatedly find the middle of an array and keep track of an upper and lower bound, until you find your item OR if your middle element becomes starts incepting the upper and lower bound.

## Data Structures
### Linked List
- A linked list contains nodes which in the context of a linked list are units that contain data, and potentially two pointers, one pointer to the next item in the list and depending on the type of linked list, a poitner to the previous item in the list. Keep in mind that in other languages besides JavaScript or Python, arrays are static, they're size doesn't grow, this is why linked list are more prevalent in these languages, because it uses pointers to other data, a set size is not required.
  - Why not use a link list over an array all the time? Because it does require more space since each node needs a pointer and a data and it takes more time to read data as you need to go through the linked list where in an array you can just pick which index
  - **Application:** Consider using a linked list when that data that is stored in the linked list needs to be accessed together. Some files are stored as linked list, their data are split into chunks and all the chunks are nodes in a linked list.
### Stack
- A type of data structure that follows a first in last out approach. Think of it as a special type of an array or linked list, where we can only look at the item that was last entered into the stack; if we wanted to look at that other items we need to remove the items on top first. It's very a limited data structure in terms of functionality, but it does provide great efficiency for the actions that  you can do, such as accessing the item pushed on top of the stack, or removing or adding a new item.
- **Application:** With such limited functionality, it might be difficult to understand what we use stacks for, but the best example is to consider the call stack. The call stack is what we use in programming to keep track of what functions we want to execute. There's a specific order we want to follow when we write functions, callback functions and recursions, and the call stack helps us maintain that by ensuring first in, last out.
### Queues
- A type of data structure that follows a first in first out approach. Similiar to a stack, it's a special type of an array or linked list (depends on how you want to implement it) where we can only access the item that was first in, and if we want to access any other items we have to remove all items before that. Again, similiar to a stack, it has very limitted functionality but it's super efficient at what it can do.
- **Application:** Essentially anywhere, where you need to prioritize things by when they come up, for example the printer when it's printing items or CPU schedule.
- Now there are variations of queues, such as: 
  - The priority queue, where we not only consider when an item was entered in the queue, but also it's priority level. With that in mind, when are removing anything priority queue we need to search through it to find the highest priority, this will have a time complexity of O(n) because you don't know which item has it and you need to go through them all.
  - The double ended queue where we don't just remove items from the beginning but from the end. You can imagine that if you do have a double ended queue, you need to have a doubly linked list. 
### Hash Tables
- A hash table is a type of data structure that implements an associative array abstract data type meaning that it maps keys to value but what sets it apart from just your regular associative array (like a javascript object, or a python dictionary) is that when you store data in a hash table, it uses a hash function to decide where the data is stored in the table. 
- The *hash function* takes a key, which can be the data, or parts of a data, and scrambles it with an algorithm to produce an index in the table, and this where the data will be stored. This has function must be consistent meaning that a key must always have the same value.
- A perfect hash function would have be written such that no key value will ever produce the same index, but this is unrealistic, the more data we have the more likely we are to run into the situation where the hash function produces the same index value for the same key - this is what is called a collision. We can approach a collision two ways:
  - We can do probing where if a collision occurs, we just find the next available spot:
    - Linear probing where we just move to the next spot in the table and see if it's available, if it's not we check the next one after.
    - Quadractic probing where we check 1 spot after, then 4 spots after, then 9, and so on and so on.
    - Double Hashing, if a collision occurs, just hash again.
  - We can also do chaining, where if a collision occurs, that new key is still linked to that index; it's just chained to the element that's already there.
  - Which way is better?
    - Probing does not require another data structure, and it allows a table to filled up more efficiently. However, that means a table can be completely filled up, and the addresses of a key is sometimes unpredictable as probing can take a key to some random value
    - Chaining allows allows a table to keep growing since values just keep getting chained on (typically using a linked list), and the values are always predicatable. Chaining does require more memory and processing since we are creating a linked list, AND sometimes certain slots in table will never get filled.
- Why is this better than just an associative array? Because we're using simple indexes to store data, it will use less memory, and we can still find our data.
- **Applications:** It's use is great for storing data and retrieiving it fast from a collection of million/billion entries, think of a spell checker. When you type a word, there will be a problem that takes whatever you typed, but it through a hash funciton and then see if it exists in a hash table containing all the known words. If it's not in the table, we know the word is spelt wrong!
