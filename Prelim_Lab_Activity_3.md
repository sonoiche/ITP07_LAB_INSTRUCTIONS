# LABORATORY ACTIVITY

**Course:** Integrative Programming  
**Activity Title:** PHP Personal Expense Tracker (Basic PHP Concepts)  
**Duration:** 2–3 Hours  
**File Name:** `expense_tracker.php`

---

## I. OBJECTIVE

The objective of this laboratory activity is to enable students to apply fundamental PHP programming concepts by developing a simple personal expense tracking program. Through this activity, students will demonstrate the use of variables, arithmetic and comparison operators, user-defined functions, indexed arrays, and associative arrays in a practical scenario. The activity aims to strengthen problem-solving skills, improve understanding of data organization and processing in PHP, and reinforce clean coding practices by creating a working server-side script that performs calculations and displays structured output in a web browser.

---

## II. OVERVIEW

In this activity, you will create a basic **Personal Expense Tracker** using PHP. Instead of storing academic data, your program will simulate a real-world budgeting scenario where daily expenses are recorded, categorized, and summarized.

You will define expenses using arrays, compute totals using operators, organize reusable logic using functions, and display summarized results in a clear and readable format. This activity focuses purely on PHP fundamentals and does not require databases, forms, or external frameworks. By the end of the activity, your program should show how PHP can process and organize real-life data through structured coding practices.

---

## III. LEARNING OUTCOMES (OBE-ALIGNED)

After completing this activity, the student should be able to:

- Apply basic PHP syntax to build a functional server-side script.
- Use variables and operators to perform data processing tasks.
- Create reusable functions to simplify program logic.
- Implement indexed and associative arrays to organize data.
- Use loops to iterate through arrays and generate structured output.
- Produce readable, organized, and maintainable PHP code.

---

## IV. INSTRUCTIONS

### General Requirements

1. Create one PHP file named:

```
expense_tracker.php
```

2. The program must run on a local PHP server (e.g., XAMPP).
3. All output must be displayed using PHP.
4. Write clean, properly indented, and readable code.

---

### Part A – Variables and Operators

1. Declare variables for the following:

- Owner Name  
- Budget Amount (monthly budget)

Example:

```php
$owner = "Juan";
$budget = 5000;
```

2. Use arithmetic operators to compute:

- Total expenses  
- Remaining balance

---

### Part B – Indexed Array (Expenses List)

1. Create an indexed array containing at least **five (5)** expense amounts.

Example:

```php
$expenses = [250, 120, 80, 450, 300];
```

2. Use a loop to:

- Display each expense  
- Compute the total expense

---

### Part C – Associative Array (Expense Categories)

1. Create an associative array containing categories and their amounts.

Example:

```php
$expenseCategories = [
    "Food" => 500,
    "Transportation" => 300,
    "Internet" => 120,
    "School Supplies" => 200
];
```

2. Display each category and amount using a loop.

---

### Part D – Functions

Create the following functions:

#### 1. `calculateTotalExpense()`

- Accept an array as parameter  
- Return the total expense

#### 2. `calculateRemainingBalance()`

- Accept budget and total expense as parameters  
- Return the remaining balance

#### 3. `displayStatus()`

- Return:
  - **"Within Budget"** if balance ≥ 0  
  - **"Over Budget"** if balance < 0  

---

### Part E – Program Output

Display the following in a clean format:

- Owner Name  
- Monthly Budget  
- List of Expenses  
- Expense Categories  
- Total Expense  
- Remaining Balance  
- Budget Status  

Example Output:

```
Owner: Juan
Monthly Budget: 5000

Expenses:
250
120
80
450
300

Expense Categories:
Food: 500
Transportation: 300
Internet: 120
School Supplies: 200

Total Expense: 1200
Remaining Balance: 3800
Status: Within Budget
```

---

## V. STARTER CODE (OPTIONAL)

You may use this starter structure:

```php
<?php

$owner = "Juan";
$budget = 5000;

$expenses = [250, 120, 80, 450, 300];

$expenseCategories = [
    "Food" => 500,
    "Transportation" => 300,
    "Internet" => 120,
    "School Supplies" => 200
];

function calculateTotalExpense($arr) {
    // your code here
}

function calculateRemainingBalance($budget, $total) {
    // your code here
}

function displayStatus($balance) {
    // your code here
}

?>
```

---

## VI. ADDITIONAL REQUIREMENTS

- You must use:
  - Variables  
  - Arithmetic operators  
  - At least 3 functions  
  - Indexed array  
  - Associative array  
  - Loop (foreach or for)

- Do not use database connections or forms.
- Focus on correct PHP logic and output formatting.

---

## VII. COMMON MISTAKES TO AVOID

- Forgetting to return values from functions.
- Mixing indexed arrays and associative arrays incorrectly.
- Not initializing totals before loops.
- Printing raw arrays instead of iterating through them.
- Poor indentation or unclear variable names.

---

## VIII. BONUS CHALLENGES (OPTIONAL)

If you finish early, try these:

1. Add an additional category summary showing which category has the highest expense.
2. Format currency using `number_format()`.
3. Display a warning message if remaining balance is below 20% of the budget.
4. Sort expenses from highest to lowest before displaying.

---

## IX. EXPECTED OUTPUT

Your program should simulate a simple budgeting system that calculates expenses and displays a summary report using PHP fundamentals.

---

## X. SUBMISSION GUIDELINES

1. Submit the following:
   - `expense_tracker.php`
   - Screenshot of output (optional if required by instructor)

2. Ensure:
   - Program runs without errors
   - Code is readable and organized
   - All required concepts are implemented

---

## XI. GRADING CRITERIA (Suggested)

| Criteria | Points |
|----------|--------|
| Correct Use of Variables & Operators | 20 |
| Proper Use of Functions | 20 |
| Indexed Array Implementation | 15 |
| Associative Array Implementation | 15 |
| Output Formatting & Logic | 20 |
| Code Readability & Structure | 10 |
| **TOTAL** | **100** |

---

### End of Laboratory Activity
