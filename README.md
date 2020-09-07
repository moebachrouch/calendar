# calendar
Programming a command line calendar using Java.

This project was done with the help of Listing 6.2 in Introduction to Java Programming by Y. Daniel Liang.

The Gregorian calendar that we use today has 12 months. A month has either:

- 30 days, or
- 31 days, or
- 28 days for February, or
- 29 days for February if the year is a leap year.
A leap year happens every 4 years (2010, 2014, 2018, etc.), except if it is divisible by 100 (1700, 1900, etc.). Years divisible by 400 are leap years (1200, 1600, 2000, etc.).

So, a leap year is:

- Divisible by 4 and not divisible by 100, or
- Divisible by 400.

Each month in the calendar is characterized by:

- The day of the week at which the month starts.
- The number of days in the month.
Getting the number of days in the month is simple. We need to know what the month is, and we need to know if the year is a leap year.

Getting the day of the week at which the month starts is slightly more complicated. There are many ways of doing this knowing the month and year, like Zeller's Congruence. The method we will be using is different. We will use a base year and determine the first day of that year. Then, we will count the number of days all the way up to the first day of the desired month of the year. Then, we can find the first day of the month as follows:

Say it is Tuesday (day 2 of the week). 8 days have passed. What day is it today?

The answer is: (2 + 8) % 7 = 3. That is a Wednesday.

We could have counted on our fingers 8 days from a Tuesday. Or, we could have said: 7 days from a Tuesday is a Tuesday, therefore 8 days from a Tuesday is a Wednesday. But to work with large numbers, we need a better method.

We know that the week system works on a cycle. Every 7 days, the day of the week repeats. To work with cycles, we use the remainder operator in Java (%). 0 % 7 = 0 (Sunday). 1 % 7 = 1 (Monday). 7 % 7 = 0 (Sunday). When we go beyond 7, things get interesting. 8 % 7 = 1 (Monday). 9 % 7 = 2 (Tuesday).

Here, we're asking: how many times does 7 go into 9? The answer is 1. But, there are 2 days remaining, hence the answer of the remainder operation is 2.

We just created a useful technique to calculate the current day of the week knowing the number of days passed, and the first day of the week for a base year:

1) Add the number of days passed since a base year to the first day of the week for the base year.
2) Divide the result by 7 and obtain the remainder, which is the current day of the week.
The base year we will use is the Unix epoch (Midnight 1 January 1970).

At this point, we have everything we need to create a calendar in Java. The calendar will first be created for an individual month and year. Then, using a loop, it will be created for all 12 months of that year.

We will take a hierarchical approach to solve this problem.

First, we need a method to print a month.

Italian Trulli

Inside this method, we will have two methods:

- A method that prints the month title. This one is pretty straightforward, and it prints the month's name and all the days of the week. To get the month name, we use a method which returns a String depending on the number of the month ("January" for 1, "February" for 2, etc.).
- A method that prints the month body. Inside this method, we will do a few things. First, we will get the start day of the month. Next, we will get the number of days in that month. Finally, we will print the body using that information.


To get the start day of the month, we use the following method:

This method sets the start day for the base year: Midnight 1 January 1970, which was a Thursday (Day 4 of the week). Then, it calculates the number of days since 1 January 1970.

In this method, we do two things:

- Add up the number of days from 1 January 1970, until 1 January of the desired year.
- Add up the number of days from 1 January of the desired year, until the the desired month of the desired year.
In this process, the program checks whether the year from 1970 is a leap year. If it is, It adds 366 to the total number of days. Otherwise, it adds 365.

The program also returns the total number of days for each month using the following method:

Now, all we have to do is create a main method and run the program. The main method will use a for loop to print the calendar for 2020. In order words, it will print every month from January 2020 to December 2020.

We can even ask the user to input a year and then print the calendar for that year.
