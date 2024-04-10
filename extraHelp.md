# Maths Hints for Stage 3
Only use these if you really need them!

## Hint for exercise 3.4: Including the time difference

This assumes you have a variable called `time` that stores the date, as shown in exercise 3.3.

To get the hour in the current time zone:

```
const hour = time.getHours();
```

To get the hour including the time difference, use the `hoursDiff` parameter:

```
const hour = time.getHours() + hoursDiff;
```

For example, Sydney is 11 hours ahead of York. If it is 9am in York, it will be 8pm in Sydney. The line of code above will return 9 + 11 = 20, which is correct.

BUT, what if the time in York is 3pm? The line of code above will return 15 + 11 = 26, which not a valid hour. You can ensure the calculated time is always valid (i.e. between 0 and 24) using the % operator:

```
const hour = (time.getHours() + hoursDiff) % 24;
```

The % (or modulo) operator returns the remainder of a division e.g. x % y will return the remainder of x / y.

If the time in York is 3pm, and the value of `hoursDiff` is 11, the above line of code is equivalent to (15 + 11) % 24, or 26 % 24. 26 / 24 is 1 with a remainder of 2. Therefore, the value of hour will be 2, which is the correct hour in Sydney if the hour in York is 15.

[Click here to return to the exercise.](README.md#exercise-34-get-the-hour-minute-and-seconds-including-any-time-difference)

## Hint for exercise 3.4: Converting the hour from the 24-hour format to the 12-hour format

The solution to this step is very similar to the solution to including the time difference in the hour.

You *could* subtract 12 from the hour if it past midday but the % operator is a simpler solution. The % operator gives you the remainder of a division. To convert a 24-hour time to a 12-hour time, you need the remainder of the 24-hour time divided by 12. Here are a few examples showing the calculation for 9am, 12pm, and 3pm:

9 / 12 is 0 with a remainder of 9. So, 9 % 12 = 9.
12 / 12 = 1 with a remainder of 0. So, 12 % 12 = 0.
15 / 12 = 1 with a remainder of 3. So, 15 % 12 = 3.

Save the result of the calculation as a new variable:

```
const convertedHour = hour % 12;
```

[Click here to return to the exercise.](README.md/#exercise-34-get-the-hour-minute-and-seconds-including-any-time-difference)

## Hint for exercise 3.5: Calculating the rotation of a hand

To calculate the rotation of *any* hand, use this formula:

```
value / maximum value * number of degrees in a circle
```

…where value is the value of the hand (e.g. the calculated hour, minutes, or seconds) and maximum value is the highest possible value for that hand (12 for hours, 60 for minutes and seconds).

Here is a worked example for the hour hand when the hour is 5:

5 / 12 * 360 = 150 degrees

[Click here to return to the exercise.](README.md/#exercise-35-move-the-hands)
