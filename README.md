# PHP Basics — Laboratory Activity

Objective
-	Guide students to create a simple PHP file that demonstrates variables, operators, functions, arrays, and associative arrays.

Overview
-	Students will create an `index.php` file that: declares variables of different types, displays them, performs arithmetic and comparisons, defines and calls a function to calculate the area of a rectangle, iterates over an indexed array of programming languages, and displays a student's associative array inside an HTML table.

Before you begin
-	Ensure PHP is installed on your machine. You can use a bundled environment (XAMPP, MAMP) or the built-in PHP server.
-	Create a project folder and open it in your editor. Save your main file as `index.php` inside the project root.

Step-by-step instructions (do not copy/paste exact code — write it yourself)
1. Create the file
-	Create a new file named `index.php` in the project folder.

2. Declare variables of different data types
-	Choose descriptive variable names and declare at least five variables using different data types:
  - a string (e.g., a student's name or a greeting)
  - an integer (e.g., age or a count)
  - a float (e.g., GPA or a price)
  - a boolean (e.g., a true/false flag)
  - an array (simple list of two or three items to begin with)
-	Hint: Use meaningful values so printed output is readable.

Example (reference — not the final solution):

```php
// choose your own names and values
$studentName = "Sam";    // string
$studentYears = 19;       // integer
$rating = 4.25;           // float
$active = false;          // boolean
$tools = ["html", "css"]; // simple array
```

3. Display values using `echo` or `print`
-	Output each variable to the browser. For booleans, convert the value to a readable text such as `true`/`false`.
-	Use string concatenation or interpolation (your preferred style) to format the output, and add HTML line breaks (`<br>`) or paragraphs so each item appears on its own line.

Example (reference):

```php
// show values in a readable way
echo "Student: " . $studentName . "<br>";
echo "Active: " . ($active ? 'yes' : 'no') . "<br>";
```

4. Arithmetic operations
-	Declare two numeric variables and compute the following using PHP arithmetic operators:
  - sum (addition)
  - difference (subtraction)
  - product (multiplication)
  - quotient (division)
-	Display each result with a short label (for example: "Sum = ..."). Try different numeric values to see how division behaves with integers and floats.

Example (reference):

```php
$n1 = 8;
$n2 = 2.5;
$s = $n1 + $n2;        // addition
$d = $n1 - $n2;        // subtraction
$p = $n1 * $n2;        // multiplication
$q = $n1 / $n2;        // division
echo "Sum: $s" . "<br>";
```

5. Comparison and logical operators
-	Compare two values using both loose equality (`==`) and strict equality (`===`) and print messages to indicate whether they are equal or not.
-	Demonstrate at least one logical expression combining conditions (for example using `&&` or `||`) and print a sentence that depends on the result.

Example (reference):

```php
$valA = 7;
$valB = "7";
if ($valA == $valB) echo "loosely equal<br>";
if ($valA === $valB) echo "strictly equal<br>"; // likely not shown

// logical example
if ($active || $rating > 4.0) echo "Meets one of the conditions";
```

6. Write the function `calculateArea($length, $width)`
-	Create a function named `calculateArea` that accepts two parameters and returns the computed area (length × width).
-	Call the function with example numeric arguments and display the returned value with an explanatory label.

Example (reference):

```php
function rectArea($l, $w) {
  return $l * $w;
}
// call it and display
$result = rectArea(7, 2);
echo "Rectangle area: " . $result . "<br>";
```

7. Indexed array of programming languages
-	Declare an indexed array containing at least five programming languages.
-	Use a `foreach` loop to iterate over the array and print each language on its own line (add simple bullets or prefixes if you like).

Example (reference):

```php
$langs = ["Ruby", "Go", "Python", "C", "PHP"];
foreach ($langs as $l) {
  echo "* " . strtoupper($l) . "<br>";
}
```

8. Associative array for student information and HTML table display
-	Create an associative array with at least three key-value pairs representing a student (for example: `name`, `age`, `course`).
-	Use a `foreach` loop to iterate over the associative array and output each key/value pair as a row in an HTML table. The table should have two columns: "Field" and "Value".
-	Hint: Use `ucfirst()` or similar to tidy up key labels when you display them.

Example (reference):

```php
$studentInfo = [
  'fullName' => 'Jordan',
  'years' => 22,
  'major' => 'IT'
];

echo "<table>";
foreach ($studentInfo as $k => $v) {
  echo "<tr><td>" . ucfirst($k) . "</td><td>" . $v . "</td></tr>";
}
echo "</table>";
```

Testing and running your code
1. Using the built-in PHP server (quick way to test):

```bash
php -S localhost:8000
```

-	Open your browser and navigate to `http://localhost:8000/index.php`.
-	If you use XAMPP/MAMP, place the file in the correct htdocs/www folder and start Apache.

Expected learning outcomes
-	Students should demonstrate an understanding of PHP variable types and basic syntax.
-	Students should be able to apply arithmetic and comparison operators and understand the difference between loose and strict equality.
-	Students should be comfortable writing simple functions and using arrays and loops.

Hints (do not give full code)
-	Break the task into small steps; implement and test each piece before moving on to the next.
-	Print intermediary values to verify types (for example, echo a value and check browser output).
-	If the boolean prints as empty or `1`, convert it to readable text before displaying.
-	If division gives an unexpected format, try casting or using float values for clearer quotient results.

Assessment checklist (for grading)
-	File `index.php` exists and runs without PHP errors.
-	At least five variables declared using the specified types.
-	Arithmetic results shown for sum, difference, product, quotient.
-	Comparison examples demonstrate both `==` and `===` behavior.
-	`calculateArea` function implemented and called; returned value printed.
-	Indexed array of ≥5 languages displayed via loop.
-	Associative array displayed in an HTML table using `foreach`.

Extensions (optional challenges)
-	Add input form fields and accept user input for the rectangle dimensions, then calculate area from submitted values.
-	Sort the array of languages alphabetically before displaying.
-	Add validation checks for numeric input and show friendly error messages.

If you want, I can review a student's completed `index.php` and provide targeted feedback (marking issues and suggestions). Good luck!
