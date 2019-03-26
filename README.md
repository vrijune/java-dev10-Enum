Industry Lab 10: More Collections, Enumerated Types, & Recursion
==========
## Exercise One: Sorting, Comparable & Comparator
In the `ex01` package, you’ll notice our familiar Shape classes once again. For this exercise, we want to sort a list of Shapes in a couple of different ways.

When you’ve completed steps 1 and 2 below, your program should compile and run without errors, and produce the output shown here:
```text
Number of shapes in set: 8
 - RegularPolygon [numSides=6, sideLength=2] has a perimeter of: 12cm
 - RegularPolygon [numSides=8, sideLength=2] has a perimeter of: 16cm
 - Rectangle [width=4, length=5] has a perimeter of: 18cm
 - Circle [radius=3.0] has a perimeter of: 18.85cm
 - RegularPolygon [numSides=4, sideLength=5] has a perimeter of: 20cm
 - Circle [radius=4.0] has a perimeter of: 25.13cm
 - Rectangle [width=3, length=10] has a perimeter of: 26cm
 - Rectangle [width=10, length=9] has a perimeter of: 38cm
 
Number of shapes in list: 10
 - Circle [radius=4.0] has 1 sides and an area of: 50.27cm^2
 - Circle [radius=4.0] has 1 sides and an area of: 50.27cm^2
 - Circle [radius=3.0] has 1 sides and an area of: 28.27cm^2
 - Rectangle [width=10, length=9] has 4 sides and an area of: 90cm^2
 - Rectangle [width=3, length=10] has 4 sides and an area of: 30cm^2
 - RegularPolygon [numSides=4, sideLength=5] has 4 sides and an area of: 25cm^2
 - Rectangle [width=4, length=5] has 4 sides and an area of: 20cm^2
 - Rectangle [width=4, length=5] has 4 sides and an area of: 20cm^2
 - RegularPolygon [numSides=6, sideLength=2] has 6 sides and an area of: 10.39cm^2
 - RegularPolygon [numSides=8, sideLength=2] has 8 sides and an area of: 19.31cm^2
 
Process finished with exit code 0
```

### Step 1: Implement Comparable<T>
If we run the main **ExerciseOne** class now, we’ll see that the program throws a **ClassCastException**. This is because we’re trying to add Shapes to a **TreeSet** in the **sortedSetExample** method. **TreeSets** automatically sort their contents according to their *natural ordering* – but at this stage, we haven’t yet defined a natural ordering for Shapes!

To do this, go to the Shape class and make it implement the **Comparable<Shape>** interface. In the compareTo method that you’ll have to implement, define a **Shape**’s natural ordering such that **Shapes** will be sorted according to their *perimeter*, in *ascending order*.

Once we correctly implement the **Comparable** interface, we should see that the **sortedSetExample** method now prints the shapes out in order of their perimeter. We should also notice something else about the *number* of shapes printed out. What do we notice, and why does it occur?

### Step 2: Sort using a Comparator<T>
Currently, in **ExerciseOne**, the **comparatorExample** method prints out the shapes in no particular order. We want to write a Comparator to define an *external ordering* for the shapes which is different to their natural ordering which we implemented in step 1 above.

We have written the beginnings of a **Comparator** implementation in the method, as an anonymous inner class. You’ll see that the implementation currently just returns 0. For this step, use the comparator to define an ordering such that Shapes are sorted first by **their number of sides (<i>ascending order</i>)** *then* by **their area (<i>descending order</i>)**. For example, a shape with 3 sides and an area of 10cm2 would “come before” a shape with 3 sides and an area of 4cm2. Both of those would “come before” any shape with more than 3 sides, regardless of its area.

Once you’ve implemented the Comparator, at the marked location in the code, make an appropriate call to **Collections.sort** to sort the **shapeList** using the **shapeComparator**.

## Exercise Two: Mapping Character Frequency in a Text Block
The program in the `ex02` package is intended to look at a given piece of text, and examine the number of times each letter (from A-Z) and number (from 0-9) appears in that text. The program should then print out this information in a table similar to the following:
```text
Char:   Frequencies:
--------------------
'A' 	135
'B' 	51
'C' 	60
'D' 	71
'E' 	253


Etc...
```

There are two incomplete methods in the **ExerciseTwo** class which you’ll implement in this exercise.

### Step 1: Fill a Map
The **getCharacterFrequencies** method is supposed to create and return a Map, relating each character to the number of times that character occurs in the text. As you can see from the code, we’re only considering characters from ‘0’ – ‘9’ and from ‘A’ to ‘Z’ (though that could easily be changed by altering or removing the if statement).

There are a few things we’ll want to do to complete this method. Firstly, where we’re declaring the frequencies Map, initialize it to an appropriate implementation class. When deciding which to use, remember that we eventually want to be displaying our frequencies in alphabetical order.

Next, we need to actually add values to our map. For each character in the input string, we want to either *i)* increment the frequency count we already have for that character, or *ii)* add an initial frequency count of 1 for that character if we haven’t encountered it before.

Finally, as a bonus, we could add any “missing” keys to the map. For example, if we were examining a string with no ‘Z’ characters, our current code wouldn’t ever add ‘Z’ to the map. We could, if we wanted to, add ‘Z’ to the map, with a frequency of 0.

### Step 2: Print the Map
In the **printFrequencies** method, print out all characters (keys) and their frequencies (values) in the given **Map**. You may iterate through the map using any technique you like in order to accomplish this.

## Exercise Three: Simple Recursion Exercises
For this exercise, answer the following problems on paper. Try to figure out the answer by hand, rather than just typing the code into your IDE and writing down the output. This is important practice for possible upcoming test questions!

1. Consider the code below. What is the return value when **foo(4)** is executed?
```java
private int foo(int x) {
   if (x <= 1) {
      	return 1;
   }
 
   return x * foo(x - 1);
}
```

2. Consider the code below.
```java
private double bar(double x, int n) {
   if (n > 1)
      	return x * bar(x, n - 1);
   else if (n < 0)
      	return 1.0 / bar(x, -n);
   else
      	return x;
}
```
  * What is the return value when **bar(2, 3)** is executed?
  * What is the return value when **bar(3, -2)** is executed?
 
3. Consider the code below. What is the problem with it?
```java
private void bad1() {
   System.out.println("This is very good code.");
   bad1();
}
```
 
4. Consider the code below. What is the problem with it?
```java
private int bad2(int n) {
   if (n == 0) {
      	return 0;
   }
 
   return n + bad2(n - 2);
}
```

5. Consider the code below:
```java
private int bad3(int n) {
	if (n == 0) {
		return 0;
	}

	return n + bad3(n + 1);
}
```
  * Write a method call to **bad3()** that will cause problems.
  * Write a method call to **bad3()** that will not cause problems.

## (Optional) Exercise Four: Writing Recursive Methods
For this exercise, complete the recursive methods in the **ExerciseFour** class in the `ex04` package. You may use the provided unit tests to check whether your methods are functioning correctly. Use recursion to complete each of these methods (even if you can think of a non-recursive way to solve them)! The methods you should complete are as follows:

1. Complete the **getSum** method, which should return the sum of all positive integers between 1 and num (inclusive).

2. Complete the **getSmallest** method, which should return the smallest element in an array of integers between the given first (inclusive) and second (non-inclusive) indices.
 
3. Complete the **printNums1** method, which should print out all the integers starting from the provided positive integer n, down to 1.
 
4. Complete the **printNums2** method, which should print out all the integers starting from 1, up to the provided positive integer n.
 
5. Complete the **countEs** method, which returns the number of ‘e’ and ‘E’ characters in the provided **String**.
 
6. Complete the **fibonacci** method, which should return the nth number in the Fibonacci sequence.
 
7. Complete the **isPalindrome** method, which should return a boolean value indicating whether the provided **String** is a palindrome.

