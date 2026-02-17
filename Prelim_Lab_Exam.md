# Prelimlab — Laboratory Exam Guidelines

A simple web application that collects a student’s name and three exam grades (Prelim, Midterm, Final), computes the average, assigns a grade equivalent, and shows whether the student passed or failed. This README gives instructions and guidelines for developing it. **Do not copy code from elsewhere; use these guidelines to write your own solution.**

---

## What You Need

- A working PHP environment (e.g. XAMPP, WAMP, MAMP, or PHP built-in server).
- A browser to open the page and submit the form.
- Basic knowledge of HTML forms, PHP superglobals, arrays, loops, and conditionals.

---

## Running the Application

1. Put your project folder where your PHP server can run it (e.g. `htdocs` or project root).
2. If using the built-in server: open a terminal in the project folder and run the command that starts the PHP development server for the current directory.
3. In the browser, go to the URL shown (usually something like `http://localhost:8000` or `http://localhost/prelimlab`).
4. You should see a form. Enter a student name and three grades, then submit to see the result.

---

## Development Guidelines (By Part)

### Part A — Form Creation

**Goal:** Build the HTML form that collects user input.

- Create a single page (e.g. `index.php`) that outputs HTML.
- Add a form that sends data using the **POST** method. Decide whether the form submits to the same page or another script; both are valid.
- Include one input for **Student Name** and three inputs for **Prelim Grade**, **Midterm Grade**, and **Final Grade**. Choose input types that fit text and numeric grades (e.g. text for name, number for grades).
- Give every input a clear, visible **label** (use the `label` element and associate it with the input so the form is accessible).
- Add a **submit** button so the user can send the form.
- Validate in your mind: when you click Submit, does the form send the four values via POST? You will use those in Part B.

**Tips:** Use meaningful `name` attributes; they become the keys in the superglobal you use for POST data. Keep labels and placeholders clear so the user knows what to enter.

**Sample (Part A only — form + inputs):** This is just a *structure example* for labels/inputs/submit. You must still implement your own processing for Parts B and C.

```html
<form method="post" action="index.php">
  <!-- Student Name -->
  <label for="student_name">Student Name</label>
  <input id="student_name" name="student_name" type="text" required>

  <!-- Grades (adjust min/max/step as your exam requires) -->
  <label for="prelim_grade">Prelim Grade</label>
  <input id="prelim_grade" name="prelim_grade" type="number" required>

  <label for="midterm_grade">Midterm Grade</label>
  <input id="midterm_grade" name="midterm_grade" type="number" required>

  <label for="final_grade">Final Grade</label>
  <input id="final_grade" name="final_grade" type="number" required>

  <button type="submit">Submit</button>
</form>
```

---

### Part B — Data Processing

**Goal:** When the form is submitted, read the values in PHP, store the three grades in an array, and compute total and average.

- At the top of your PHP script (before any HTML), check that the request method is POST and that the expected POST keys exist. Only run the processing logic when the form was actually submitted.
- Use the appropriate **PHP superglobal for POST data** to get the submitted student name and the three grades. Sanitize or validate as needed (e.g. trim the name, ensure grades are numeric).
- Store the **three grades in one indexed array** (e.g. first element = Prelim, second = Midterm, third = Final). Do not use separate variables for the loop requirement.
- Use a **foreach** loop over that array to add each grade to a running total. After the loop, you should have the sum of the three grades.
- Compute the **average** with the formula:  
  **Average = (Prelim + Midterm + Final) / 3**  
  So: total from the loop divided by 3. Keep the result in a variable for Part C.

**Tips:** Convert grade inputs to numbers (integer or float) before storing or calculating. Decide where to put the processing (same file vs. separate file) and keep the logic in one clear block.

---

### Part C — Conditional Evaluation

**Goal:** From the average, determine the grade equivalent (using if-elseif-else) and pass/fail status (using a ternary operator).

- **Grade equivalent:** Use one **if-elseif-else** structure. Each branch should check the computed average against a range (e.g. 90–100, 85–89, 80–84, etc.) and assign the corresponding grade equivalent (e.g. 1.0, 1.5, 2.0, 2.5, 3.0, 5.0 or the scale given in your exam). Follow the **grading table provided in your problem statement** exactly.
- **Passed or Failed:** Use a **ternary operator** (condition ? value_if_true : value_if_false) to set a single variable to either "Passed" or "Failed" based on the average (e.g. passing if average is at least 75 or 70, depending on the problem).
- Store both the grade equivalent and the pass/fail status in variables so you can output them in the result section.

**Tips:** Order the if-elseif conditions from highest range to lowest (or lowest to highest consistently) so only one branch runs. Use the same passing threshold in the ternary as in your grading table.

---

## Showing the Result

- After processing, you need to **output** the student name, the three grades, total, average, grade equivalent, and pass/fail status.
- Only show the result block when the form was submitted and processing ran successfully (e.g. check a flag or that your result variable is set).
- Escape output (e.g. student name) when printing to HTML to avoid XSS. Use the PHP function intended for HTML context.

---

## Checklist Before Submitting

- [ ] Form uses POST and has labeled fields for Student Name, Prelim, Midterm, and Final.
- [ ] Submitted values are read from the correct superglobal.
- [ ] The three grades are stored in one indexed array and the total is computed with a foreach loop.
- [ ] Average is computed as (Prelim + Midterm + Final) / 3.
- [ ] Grade equivalent is determined with if-elseif-else according to the given grading table.
- [ ] Passed/Failed is determined with a ternary operator.
- [ ] Result is shown only after a valid form submission, with safe output.

---
