# NewCodingBot
Creating New repository to submit Assignment to A Company

import csv

# Function to check if an employee has worked for 7 consecutive days
def has_worked_consecutive_days(shifts):
    consecutive_days = 0
    for shift in shifts:
        if shift == '1':
            consecutive_days += 1
            if consecutive_days == 7:
                return True
        else:
            consecutive_days = 0
    return False

# Function to check if an employee has less than 10 hours of time between shifts but greater than 1 hour
def has_short_breaks(shifts):
    last_end_time = None
    for shift in shifts:
        if shift == '1':
            if last_end_time is not None and last_end_time < 10:
                return True
        last_end_time = 0 if shift == '0' else last_end_time + 1
    return False

# Function to check if an employee has worked for more than 14 hours in a single shift
def has_long_shift(shifts):
    shift_hours = 0
    for shift in shifts:
        if shift == '1':
            shift_hours += 1
            if shift_hours > 14:
                return True
        else:
            shift_hours = 0
    return False

# Open the CSV file with employee records
with open('employee_records.csv', 'r') as file:
    reader = csv.reader(file)
    next(reader)  # Skip the header row
    
    for row in reader:
        name = row[0]
        shifts = row[1:]  # Assuming the shifts are in columns 2 onwards
        
        if has_worked_consecutive_days(shifts):
            print(f"{name} has worked for 7 consecutive days.")
        if has_short_breaks(shifts):
            print(f"{name} has less than 10 hours of time between shifts but greater than 1 hour.")
        if has_long_shift(shifts):
            print(f"{name} has worked for more than 14 hours in a single shift.")

# You can create a public GIT repository and push this codebase to it as requested.
