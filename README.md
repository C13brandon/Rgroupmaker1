# Rgroupmaker1

import random  

# Original list of students
original_students = [
    "Chris", "John", "yahkin", "Daniel", "Joshua",
    "Malachi", "Zechariah", "Peter", "Isaiah", "Titus",
    "Mark", "Luke", "Ruth", "Noah", "Samuel",
    "Ezra", "Jerimiah", "Ezekiel", "Joel", "Job"
]

# List to keep pairs of students who can't be together
exceptions = []

# Ask the user if they want to add exceptions
answer = input("Do you want to enter exceptions? (yes/no): ").lower()  # gets user input and makes it lowercase

# If the user decides yes, allow them to enter restricted pairs
if answer == "yes":  # checks if the user said yes
    print("Enter names of two students who CANNOT be together.")
    print("Capitalize ALL names that are entered.")

    while True:  # keeps repeating until the user says to stop
        student1 = input("First student name: ")  # asks for the first student name

        # Check if student exists in the list
        if student1 not in original_students:  # checks if the student is not in the class list
            print("Error: That student is not in the list. Please try again.")
            continue  # skips back to the top of the loop

        student2 = input("Second student name: ")  # asks for the second student name

        if student2 not in original_students:  # checks if the second student is not in the class list
            print("Error: That student is not in the list. Please try again.")
            continue  # skips back to the top of the loop

        # Add the pair
        exceptions.append((student1, student2))  # adds the pair into the exceptions list

        # Ask if user wants to enter another pair
        more = input("Do you want to enter another exception pair? (yes/no): ").lower()  # asks if the user wants to keep adding pairs
        if more != "yes":  # checks if the user did not say yes
            break  # ends the exception loop

# Main loop to keep creating groups if the user wants to
while True:  # keeps the whole grouping program running until the user says no
    # Ask for the group size
    group_size = int(input("\nHow many students per group? "))  # gets group size and turns it into a number

    while True:  # keeps reshuffling until a valid set of groups is found
        # Copy and shuffle the student names
        students = original_students.copy()  # makes a copy of the original student list
        random.shuffle(students)  # randomly mixes up the students

        groups = []  # empty list to store the finished groups
        index = 0  # starts at the first student in the list

        # Count total students
        student_count = 0  # starts student count at 0
        for s in students:  # goes through each student in the list
            student_count += 1  # adds 1 each time to count students

        # Create groups
        while index < student_count:  # keeps going until all students are placed in groups
            group = students[index:index + group_size]  # takes part of the list to make one group
            groups.append(group)  # adds that group to the groups list
            index += group_size  # moves to the next set of students

        # Check if groups are valid
        valid = True  # assumes the groups are okay unless a bad pair is found

        for group in groups:  # checks each group one at a time
            for s1, s2 in exceptions:  # checks each exception pair
                if s1 in group and s2 in group:  # sees if both restricted students are in the same group
                    valid = False  # marks the grouping as invalid
                    break  # stops checking once a bad pair is found
            if not valid:  # checks if the groups are invalid
                break  # stops checking more groups

        # Stop reshuffling if valid groups are found
        if valid:  # checks if the groups passed all the rules
            break  # stops reshuffling and keeps these groups

    # Print final groups
    print("\nFinal Groups:")

    group_number = 1  # starts numbering the groups at 1
    for group in groups:  # goes through each group
        print("Group", group_number, ":", group)  # prints the group number and students in it
        group_number += 1  # adds 1 to move to the next group number

    # Ask if user wants to repeat
    again = input("\nDo you want to create another grouping? (yes/no): ").lower()  # asks if user wants to run the program again
    if again != "yes":  # checks if the user did not say yes
        print("Program ended.")
        break 
