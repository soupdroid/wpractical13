# Practical 13 (week 7, practical 1) - JavaScript Fundamentals

The aim of this week's practical is to get you up to speed on the fundamentals of DOM manipulation and modern ES6 JavaScript. These instructions are looooong but that's because it provides a lot more detail on the steps than we normally give you!

## Stage 1: DOM manipulation with JavaScript

### Exercise 1.1: Running JavaScript in the Chrome Console
Run the index.html file in the stage1-2 folder in Chrome.

Next, open the Chrome console. There are a few ways to do this. One way is to right-click on the webpage and choose "Inspect" from the contextual menu. Then, in the Developer Tools pane, select the Console tab, which should be right next to the Elements tab. When you open the console, you might see errors or warnings. You can ignore these. 

You will write snippets of JavaScript in the console to assess the composition of the page. Type JavaScript in the console to answer each of the questions below. You could answer all questions by just looking at the code but the goal here is to try out selecting DOM elements with JavaScript.

1.	**How many paragraphs does the page have?** Type `document.getElementsByTagName('p');` into the console, then press Enter. To type in the console, put your cursor by the little blue carat (>). This will print HTMLCollection followed by a number. The number is the number of elements retrieved by the method i.e., if you see HTMLCollection(2), that means there are 2 paragraphs in the page. An HTMLCollection is effectively an array that stores only HTML elements. 

Note: running JS in the console is a bit different to running a JS script. The console is known as a REPL environment (Read-Evaluate-Print Loop)—this means that the result of any statement is printed to the console. In a script to be included in a web page, you would want to save the result to a variable.

2.	**Does the page use any semantic elements other than those for text display?** Here, we're looking for elements like header, main, nav, article etc. To answer this question, you will need to adapt the code you used for the previous question.

3.	**How many children does the element with the id "more-content" have?** Before you can count the children, you will need to select the "more-content" element. Use the `document` method `getElementById()` and save it to a variable. You can access the child elements of any selected element using the `children` property. For example, if the selected element is stored in a variable called `moreContent`, you can access its children by typing `moreContent.children`. This will return an HTMLCollection. You will be able to see the number of children returned in the console but if you would like to get the actual number rather than the collection, use the `length` property e.g. `moreContent.children.length`.

### Exercise 1.2: DOM manipulation - Adding and removing elements

Try using JavaScript in the console to add the following paragraph to the `<aside>` element:

```<p>I'm a new paragraph!</p>```

Here are the steps:

- Use an appropriate method to select the `<aside>`. Remember that `getElementsById()` returns a single element but all other element selection methods return an array.
- There are two ways to add new elements: as a string (simplest) or by creating a new element (most efficient for the browser). Try either approach. Or both.

You should be able to see the paragraph in your browser. If you can't see it, look for it in the inspect tab. If the paragraph has not been added, check that you have correctly selected the `<aside>` element to add it to.  

Once you have successfully added the paragraph to the page, use JavaScript to remove it.

### Stage 1.3: DOM manipulation - Changing element styles

Your final DOM manipulation task is to use JavaScript to replace / add CSS on the webpage via the Chrome console. You will need to select one or more elements to modify e.g. all paragraphs. You can view the existing CSS of an element using its style property. For example, this is the code I used to inspect the style of the first paragraph on the webpage:

```
const paragraphs = document.getElementsByTagName('p');
paragraphs[0].style;
```

The code above prints all style properties associated with the element, even if they have not been set. Notice that CSS properties that contain hyphens are written in camelCase instead. For example, the CSS property background-color is backgroundColor in JavaScript. To change the value of any property, use the following template:

```
element.style.propertyName = "new value";
```

For example, I used the following code to change the font of all paragraphs to Comic Sans:

```
for (let para of paragraphs) {
    para.style.fontFamily = "Comic Sans MS";
}
```

Try changing at least 3 CSS properties for some of the elements—see how much of a mess you can make of the page!

## Stage 2: Using JavaScript files
### Exercise 2.1: Create a script file and connect it to the HTML
In the stage1-2 folder, create a file called main.js and add the following line of code:

```
console.log("Hello, World!");
```

Connect it to index.html by adding the following tag as the last child element in the `<body>`.

```
<script src="main.js"></script>
```

`console.log("message here")` is the JavaScript equivalent of `println()` in Processing. A key difference is that any messages you print will show up in the *browser console*, not VS Code. Check your console—you should see "Hello, World!".

Remove the `console.log()` and add some code that will replace the placeholder text in the navigation list items with real links. Where the links lead to to doesn't matter—the main goal is to manipulate the DOM with JavaScript.

Here are some useful pages to help you with the syntax:
- [W3Schools: Selecting DOM elements](https://www.w3schools.com/js/js_htmldom_elements.asp)
- [W3Schools: for of loop](https://www.w3schools.com/js/js_loop_forof.asp)
- [W3Schools: adding DOM elements](https://www.w3schools.com/js/js_htmldom_html.asp)

## Stage 3: Animating a webpage with JavaScript
This stage is **very** challenging if you are new to JavaScript, so there is a lot of detail in the instructions. You can also find extra hints and guidance in the [extraHelp.md](./extraHelp.md) page.

You will use JavaScript to animate analogue clock faces to display the time in two different time zones. A video of the final animation is included in this repo. Each exercise below takes you through one aspect of the task. Within each exercise, you will find links to extra help on the maths involved but try not to use it until you've attempted it on your own! 

### Exercise 3.1: Familiarise yourself with the HTML and CSS
Open stage3/index.html in Chrome. You should see two analogue clock faces, both displaying 12 o'clock. Eventually, you will use JavaScript to: 

- Get the current time in York and calculate the time in Sydney.
- Calculate the position of each clock hand.
- Update the CSS to move the hands.
- Display AM or PM in place of the three dots on each clock.
- Repeat the above once a second.

Before you start writing JavaScript, you'll need to understand the existing HTML and CSS so you know what you're working with. Using Chrome Dev Tools / and or the code itself, find and note down the following:

- What are the ID values for each clock? Each clock has a unique ID that can be used to select the entire clock face.
- What are the ID and class values of the div containing the three dots (…) in each clock face?
- What are the class values for the clock hands?

The key CSS property for this exercise is `transform`. This property allows you to translate and rotate HTML elements (and other transformations too!). It is currently used to position the "ticks"—the lines that represent numbers on the clock face. In the CSS file (or using the Chrome inspect tool), find a class associated with one of the ticks e.g. `three` or `four`. Look at the `transform` property. Notice that is translating the tick by 100px on the x-axis as well as rotating it. The reason for the rotation is probably obvious, but the translation might not be. Try temporarily removing the transformation to see its effect.

Next, look at the `hand` class, which sets the CSS properties shared by all clock hands. Notice that it also uses `translateX`. Again, temporarily remove this property to see its effect. In the exercises below, you will move the clock hands by setting the `translateX` and `rotate` values of the transform property.

### Exercise 3.2: Create an external script file

In VS Code, open the starter code folder and create a new file called main.js. This file should be in the same folder as the HTML and CSS files. Don't forget the .js extension!

Connect your new script file to the HTML:

```
<script src='main.js'></script>
```

You will be manipulating the DOM with JavaScript so it is important that this `<script>` element goes at the end of the `<body>` -- it should be the very last element before the closing body tag, `</body>`.

Run the HTML in Chrome and open the console. This will show any messages printed to the console. Try printing something from your new script file. If you don't see anything in your browser console, try refreshing. When you've confirmed it's working, remove the `console.log()` statement.

### Exercise 3.3: Outline a function to get the current time
In your script file, write the outline of a function called `updateClock` that has two parameters, `clockId` and `hoursDiff`. When you eventually call this function to set the time on a single clock, you will pass the HTML ID of the clock as the first argument, and the time difference in hours from the current time zone.  For example:
```
updateClock("york", 0);
updateClock("sydney", 11);
```

JavaScript provides a `Date` object, which gets the current date and time in the client's time zone. Add the following statement inside your function:

```
const time = new Date();
```

…and print it to the console using `console.log()`.

You won't see anything in the Chrome console yet because you haven't called the function. Call the function twice at the bottom of your script (for York and Sydney, code above). You will see something along the lines of:

Fri Feb 03 2023 07:32:48 GMT+0000 (Greenwich Mean Time)

### Exercise 3.4: Get the hour, minute, and seconds including any time difference

You only need the time aspect of the date to set the clock. Luckily, the `Date` object in JavaScript provides methods to get just part of the date. [Look at the Date reference](https://www.w3schools.com/jsref/jsref_obj_date.asp) and identify the methods that will get just the hour, just the minutes, and just the seconds of the current time. Save each of these components as a variable inside your function.

When you save the hour, you will need to include the time difference passed to the function (the `hoursDiff` parameter). 

The hour is returned in the 24-hour time format, e.g., 5pm is 17, but the clock face is in the 12-hour format. You will need to convert the hour to 12-hour format. Save the 12-hour version in a separate variable as you will need the 24-hour version to work out if it is AM or PM in a later exercise. Try to do this conversion in one line using the % operator, rather than using a conditional.

Big hints are available for [calculating the time difference](./extraHelp.md#hint-for-exercise-34-including-the-time-difference) and [converting the hour to the 12-hour format](extraHelp.md#hint-for-exercise-34-converting-the-hour-from-the-24-hour-format-to-the-12-hour-format). Try not to look at these until you've attempted to work it out on your own!

Print each component (converted hours, minutes, seconds) to the console to check they look right.

### Exercise 3.5: Move the hands

Still working inside your function, use the `clockId` parameter and the `document.getElementById()` method to select a clock and save it as a variable:

```
const clock = document.getElementById(clockId);
```

Next, you will move the hour hand. First, you need to select the hand. As the hands don't have IDs, you will need to use a class to select it. All hands have class "hand", but only hour hands have class "hour"—this is the class to use:

```
clock.getElementsByClassName("hour");
```

Most of the examples you have seen before start with `document`. The code above will only look for matching elements nested inside the previously selected clock. `getElementById` returns a single element but `getElementsByClassName` returns an HTMLCollection, so you're not done yet. Based on the HTML, we know there is exactly one hour hand in each clock, so we can safely select the first element in the HTMLCollection:

```
clock.getElementsByClassName("hour")[0];
```

Now you're ready to set the `transform` property on the hour hand. The resulting code will look like this:

```
clock.getElementsByClassName("hour")[0].style.transform = "translateX(100px) rotate(" + ROTATION + "deg)";
```

…where `ROTATION` is the rotation amount in degrees. Your job is to calculate the rotation using the 12-hour formatted hour from the previous exercise. A hint is available in [extraHelp.md](./extraHelp.md#hint-for-exercise-35-calculating-the-rotation-of-a-hand). As you'll need to repeat a similar calculation for the minute and second hands, consider putting this calculation into another function to reduce repetition in your code.

### Exercise 3.6: Add the AM / PM label

Still working inside your `updateClock` function, select the AM/PM div inside the clock face. From exercise 3.1, you should know that each of these divs has a unique ID. Your code will need to work for *either clock*. You can use the `clockId` parameter to work out the ID of the AM/PM label that you want to change. No hints are provided here—you can concatenate a variable and a string the same way that you would in Processing or C#. 

Set the `innerText` (or `innerHTML`) property of the current clock's AM / PM div to display "AM" if it's the morning and "PM" if it's the afternoon. Try using a ternary rather than an if statement. You will have seen a ternary in Programming for Digital Media but you might not have written one yourself. The statement should look something like this:

'''
selectedElement.innerText = boolean_expression ? "value if true" : "value if false";
'''

### Exercise 3.7: Update the clocks every second

At this stage, you should have two clocks showing the correct time in York and Sydney when the page is first loaded. Next, you will animate the clocks to continuously show the right time by calling `updateClock` every second.

JavaScript provides two super useful functions for executing some code after a certain elapsed time: [`setTimeout()`](https://www.w3schools.com/jsref/met_win_settimeout.asp) and [`setInterval()`](https://www.w3schools.com/jsref/met_win_setinterval.asp). Both functions take another function as the first argument, and a time interval in milliseconds as the second argument. Passing a function to a function may seem weird but this is a common pattern in JavaScript. The main difference between the two functions is that `setTimeout()` runs once when the time runs out while `setInterval()` will repeat forever unless it's manually cancelled. As we want our clock to update every second, we will use `setInterval()`.

You might be tempted to use `setInterval()` like this:

```
setInterval(updateClock("york", 0), 1000);
setInterval(updateClock("sydney", 11), 1000);
```

This code looks like it should update each clock every 1000 milliseconds (1000 ms = 1 s) but it won't work. When passing a function as an argument, you should only use its name (e.g. `updateClock`). If you call the function (i.e. use parentheses), as shown above, JavaScript will execute it immediately and not call it when the timer runs out. This is a problem when you need to pass arguments to the function, as we do.
The solution to this is to use an anonymous function, so called because it does not have a name. Here is an example using traditional function syntax:

```
// An anonymous traditional function:
function () { 
    // Function contents here
}
// An anonymous function passed to setInterval()
setInterval(function () {
    // Call the function with arguments here
}, 1000);
```

The anonymous function will now be called every 1000 milliseconds. Here is the complete code to update both clocks using `setInterval()`:

```
setInterval(function () {
    updateClock("york", 0);
    updateClock("sydney", 11);
}, 1000);
```

(Optional) Stage 4: JavaScript extension activities

If you would like more practice with JavaScript, try these three exercises.

(Optional) Exercise 4.1: Change a clock's colour scheme according to time of day

Use JavaScript to change the colour scheme of an individual clock to visually indicate if it is day or nighttime. You can choose day / night boundaries that make sense to you. For example, you might decide that night is from 9pm to 8am.

(Optional) Exercise 4.2: Add more clocks with JavaScript
Use JavaScript to add more clocks displaying the times of cities in different time zones. 

(Optional) Exercise 4.3: Use JavaScript to display the real date and time on the York University Press site
Go back to the last version of the York University Press site and replace the hard-coded string date in the header with the real date and time using JavaScript.
