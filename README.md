This program is an interactive salary calculator that:

Collects an employee’s personal and work details.

Validates inputs like name, age, and date of birth (DOB).

Accepts various formats for the month (e.g. "jan", "03", "march", etc.).

Calculates salary based on working days, daily wage, and leave taken.

Deducts salary for extra leave (if more than 3 days).

Adds a ₹1000 bonus if the person's birthday falls in the salary month.

Displays the salary along with the current date and time.


Robust Input Validation

The user is allowed up to 3 attempts for each input (like name, DOB, etc.).

Ensures only valid values are accepted — e.g., age must be a number and under 60, working hours must be ≤ 8, and name must contain only letters.

Flexible Month Entry

The user can enter the month in many ways: "jan", "janu", "03", "3", "march", etc.

The program maps these to full month names using aliases.

Date of Birth Handling

Asks for DOB in the format dd-mm-yyyy.

From this, it calculates the actual age of the user.

If the user is under 18, the program exits early with a warning.

Salary Calculation

The number of working days is computed as total days in the selected month minus leave days.

If the user takes more than 3 leave days, extra days are deducted from salary.

Daily salary is multiplied by valid working days to compute total salary.

Birthday Bonus

If the employee’s birthday month matches the salary month, the program:

Wishes them "Many more happy returns of the day".

Adds ₹1000 to their final salary.

Final Output

Prints the total salary, clearly formatted with the employee's name, the chosen month and year.

Also shows the real current date and time when the calculation was performed.
