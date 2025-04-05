import os

def clear_screen():
    os.system('cls' if os.name == 'nt' else 'clear')

def load_students():
    students = []
    if os.path.exists("students.txt"):
        with open("students.txt", "r") as file:
            for line in file:
                students.append(line.strip().split(","))
    return students

def save_students(students):
    with open("students.txt", "w") as file:
        for student in students:
            file.write(",".join(student) + "\n")

def add_student():
    students = load_students()
    name = input("Enter student name: ")
    age = input("Enter student age: ")
    grade = input("Enter student grade: ")
    students.append([name, age, grade])
    save_students(students)
    print("Student added successfully!")

def view_students():
    students = load_students()
    if not students:
        print("No students found.")
        return
    print("\nList of Students:")
    print("Name".ljust(15) + "Age".ljust(5) + "Grade")
    print("-" * 25)
    for student in students:
        print(student[0].ljust(15) + student[1].ljust(5) + student[2])

def update_student():
    students = load_students()
    name = input("Enter student name to update: ")
    for student in students:
        if student[0] == name:
            student[1] = input("Enter new age: ")
            student[2] = input("Enter new grade: ")
            save_students(students)
            print("Student updated successfully!")
            return
    print("Student not found.")

def delete_student():
    students = load_students()
    name = input("Enter student name to delete: ")
    for student in students:
        if student[0] == name:
            students.remove(student)
            save_students(students)
            print("Student deleted successfully!")
            return
    print("Student not found.")

def main():
    while True:
        clear_screen()
        print("Student Management System")
        print("1. Add Student")
        print("2. View Students")
        print("3. Update Student")
        print("4. Delete Student")
        print("5. Exit")
        choice = input("Enter choice: ")
        if choice == "1":
            add_student()
        elif choice == "2":
            view_students()
        elif choice == "3":
            update_student()
        elif choice == "4":
            delete_student()
        elif choice == "5":
            break
        else:
            print("Invalid choice, try again.")
        input("Press Enter to continue...")

if __name__ == "__main__":
    main()
