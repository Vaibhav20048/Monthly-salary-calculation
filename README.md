def get_attempts(func, *items, **extra):
    for _ in range(3):
        result = func(*items, **extra)
        if result is not None:
            return result
    print("Too many attempts.")
    return None 

def validate_name():
    name = input("Enter your name: ")
    if not name.isalpha():
        print("Name should only contain letters")
        return None
    return name

def validate_number(prompt, max_value=None):
    num = input(prompt)
    if not num.isdigit():
        print("The input must be a number")
        return None
    num = int(num)
    if max_value is not None and num > max_value:
        print("The input should not exceed the max value", max_value)
        return None
    return num

def month_alias():
    month_names = [
        "January", "February", "March", "April", "May", "June",
        "July", "August", "September", "October", "November", "December"
    ]
    month_map = {}
    for i, full_name in enumerate(month_names, start=1):
        month_map[full_name] = [str(i), str(i).zfill(2), full_name.lower()]
        for j in range(3, len(full_name) + 1):
            month_map[full_name].append(full_name[:j].lower())
    return month_map

def validate_month(month_map):
    user_input = input("Enter a month: ").strip().lower()
    for month, aliases in month_map.items():
        if user_input in aliases:
            return month
    print("The input is not a valid month")
    return None

def validate_leap_year(year):
    return (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0)

def validate_days_month(month, year):
    month_days = {
        "January": 31,
        "February": 29 if validate_leap_year(year) else 28,
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
    return month_days[month]

def calculate_salary():
    name = get_attempts(validate_name)
    age = get_attempts(validate_number, "Enter your age: ", max_value=60)
    working_hours = get_attempts(validate_number, "Enter your working hours: ", max_value=8)
    month_map = month_alias()
    month = get_attempts(validate_month, month_map)
    year = get_attempts(validate_number, "Enter the year: ")
    total_days = validate_days_month(month, year)
    per_day_salary = get_attempts(validate_number, "What is your daily salary: ")
    leave_days = get_attempts(validate_number, "How many days did you take leave: ")
    if leave_days > total_days:
        print("Leave days cannot be more than the number of days in the month")
    elif leave_days > 3:
        print("You should not take leave for more than 3 days")
    working_days = total_days - leave_days
    total_salary = working_days * per_day_salary
    print(name, "'s total salary for", month, year, "is:", total_salary)
calculate_salary()
