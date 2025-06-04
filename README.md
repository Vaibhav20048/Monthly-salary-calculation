def validate_name():
    name = input("Enter your name: ")
    if not name.isalpha():
        print("Name should only contain letters")
    return name

def validate_number(valid, max_value=None):
    num1 = input(valid)
    if not num1.isdigit():
        print("It must be a number")
    num1 = int(num1) 
    if max_value and num1 > max_value:
        print("It should not exceed",max_value)
    return num1

def validate_month_alias():
    month_names = [
        "January", "February", "March", "April", "May", "June",
        "July", "August", "September", "October", "November", "December"
    ]
    month_diff = {}
    for i, month_name in enumerate(month_names, start=1):
        num = str(i)
        num_padded = num.zfill(2)
        short = month_name[:3].lower()
        full = month_name.lower()
        month_diff[month_name] = [
            num, num_padded, short, full,
            short.upper(), full.upper(), month_name, month_name[:3], month_name[:3].upper()
        ]
    return month_diff

def validate_month(month_diff):
    user_input = input("Enter a month: ").strip().lower()
    for month, aliases in month_diff.items():
        if user_input in [alias.lower() for alias in aliases]:
            return month
    print("Invalid month")

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
    name = validate_name()
    age = validate_number("Enter your age: ", max_value=60)
    working_hours = validate_number("Enter your working hours: ", max_value=8)
    month_diff = validate_month_alias()
    month = validate_month(month_diff)
    year = validate_number("Enter the year: ")
    total_days = validate_days_month(month, year)
    per_day_salary = validate_number("What is your daily salary: ")
    leave_days = validate_number("How many days did you take leave: ")
    if leave_days > total_days: {
        print("Leave days cannot be more than number of days of a month")
    }
    elif leave_days > 3: {
        print("You should not take leave for more than 3 days")
    }
    working_days = total_days - leave_days
    total_salary = working_days * per_day_salary
    print(name,"'s total salary for ",month ,year ,"is:", total_salary)
calculate_salary()
