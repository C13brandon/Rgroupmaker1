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
answer = input("Do you want to enter exceptions? (yes/no): ").lower()

# If the user decides yes, allow them to enter restricted pairs
if answer == "yes":
    print("Enter names of two students who CANNOT be together.")
    print("Capitalize ALL names that are entered.")

    while True:
        student1 = input("First student name: ")

        # Check if student exists in the list
        if student1 not in original_students:
            print("Error: That student is not in the list. Please try again.")
            continue

        student2 = input("Second student name: ")

        if student2 not in original_students:
            print("Error: That student is not in the list. Please try again.")
            continue

        # Add the pair
        exceptions.append((student1, student2))

        # Ask if user wants to enter another pair
        more = input("Do you want to enter another exception pair? (yes/no): ").lower()
        if more != "yes":
            break

# Main loop to keep creating groups if the user wants to
while True:
    # Ask for the group size
    group_size = int(input("\nHow many students per group? "))

    while True:
        # Copy and shuffle the student names
        students = original_students.copy()
        random.shuffle(students)

        groups = []
        index = 0

        # Count total students
        student_count = 0
        for s in students:
            student_count += 1

        # Create groups
        while index < student_count:
            group = students[index:index + group_size]
            groups.append(group)
            index += group_size

        # Check if groups are valid
        valid = True

        for group in groups:
            for s1, s2 in exceptions:
                if s1 in group and s2 in group:
                    valid = False
                    break
            if not valid:
                break

        # Stop reshuffling if valid groups are found
        if valid:
            break

    # Print final groups
    print("\nFinal Groups:")

    group_number = 1
    for group in groups:
        print("Group", group_number, ":", group)
        group_number += 1

    # Ask if user wants to repeat
    again = input("\nDo you want to create another grouping? (yes/no): ").lower()
    if again != "yes":
        print("Program ended.")
        break
