def get_attempts(validation_function, *items, **extra):
    for _ in range(3):
        result = validation_function(*items, **extra)
        if result:
            return result
    print("Too many invalid attempts.")

def validate_name():
    name = input("Enter your name: ")
    if name.isalpha():
        return name
    print("Name should only contain letters")

def validate_number(valid, max_value=None):
    value = input(valid)
    if value.isdigit():
        number = int(value)
        if max_value is None or number <= max_value:
            return number
        print("Should not exceed", max_value)
    else:
        print("Input must be a number")

def month_mapping():
    month_names = [
        "January", "February", "March", "April", "May", "June",
        "July", "August", "September", "October", "November", "December"
    ]
    mapping = {}
    for i, month in enumerate(month_names, 1):
        number_str = str(i)
        padded = number_str.zfill(2)
        aliases = {month.lower(), month[:3].lower(), month[:4].lower(),month[:20].lower(), number_str, padded}
        for alias in aliases:
            mapping[alias] = month
    return mapping

def validate_month(month_map):
    user_input = input("Enter a month: ").strip().lower()
    if user_input in month_map:
        return month_map[user_input]
    print("Invalid month input")

def leap_year(year):
    return (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0)

def days_in_month(month, year):
    days_by_month = {
        "January": 31,
        "February": 29 if leap_year(year) else 28,
        "March": 31,
        "April": 30,
        "May": 31,
        "June": 30,
        "July": 31,
        "August": 31,
        "September": 30,
        "October": 31,
        "November": 30,
        "December": 31
    }
    return days_by_month[month]

def calculate_salary():
    name = get_attempts(validate_name)
    if not name:
        return
    age = get_attempts(validate_number, "Enter your age: ", max_value=60)
    if not age:
        return
    working_hours = get_attempts(validate_number, "Enter your working hours: ", max_value=8)
    if not working_hours:
        return
    month_map = month_mapping()
    month = get_attempts(validate_month, month_map)
    if not month:
        return
    year = get_attempts(validate_number, "Enter the year: ")
    if not year:
        return
    total_days = days_in_month(month, year)
    daily_salary = get_attempts(validate_number, "Enter your daily salary: ")
    if not daily_salary:
        return
    leave_days = get_attempts(validate_number, "How many days did you take leave: ")
    if not leave_days:
        return
    if leave_days > total_days:
        print("Leave days cannot exceed the number of days in the month.")
        return
    if leave_days > 3:
        print("The salary will be deducted for each day after the 3 day limit for leave.")
    leave_limit = 3
    salary_deduct_leave = max(leave_days - leave_limit, 0)
    total_salary = total_days * daily_salary - salary_deduct_leave * daily_salary
    print(name, "'s total salary for", month, year, "is:", total_salary)
calculate_salary()
