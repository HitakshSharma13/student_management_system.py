# Student Management System

# Define a class for the student
class Student:
    def __init__(self, roll_no, name, age, course):
        self.roll_no = roll_no
        self.name = name
        self.age = age
        self.course = course

# Define a class for the Student Management System
class StudentManagementSystem:
    def __init__(self):
        self.students = []

    def add_student(self, student):
        self.students.append(student)
        print("Student added successfully.")

    def view_all_students(self):
        if not self.students:
            print("No students in the system.")
            return
        for student in self.students:
            print(f"Roll No: {student.roll_no}, Name: {student.name}, Age: {student.age}, Course: {student.course}")

    def search_student(self, roll_no=None, name=None):
        for student in self.students:
            if student.roll_no == roll_no or student.name.lower() == name.lower():
                print(f"Found: Roll No: {student.roll_no}, Name: {student.name}, Age: {student.age}, Course: {student.course}")
                return student
        print("Student not found.")
        return None

    def update_student(self, roll_no, name=None, age=None, course=None):
        student = self.search_student(roll_no=roll_no)
        if student:
            if name:
                student.name = name
            if age:
                student.age = age
            if course:
                student.course = course
            print("Student updated successfully.")

    def delete_student(self, roll_no):
        student = self.search_student(roll_no=roll_no)
        if student:
            self.students.remove(student)
            print("Student deleted successfully.")

# Function to display the menu
def menu():
    print("\n--- Student Management System ---")
    print("1. Add Student")
    print("2. View All Students")
    print("3. Search Student")
    print("4. Update Student")
    print("5. Delete Student")
    print("6. Exit")

# Main program
if __name__ == "__main__":
    system = StudentManagementSystem()

    while True:
        menu()
        choice = input("Enter your choice: ")

        if choice == '1':
            roll_no = input("Enter Roll No: ")
            name = input("Enter Name: ")
            age = input("Enter Age: ")
            course = input("Enter Course: ")
            student = Student(roll_no, name, age, course)
            system.add_student(student)

        elif choice == '2':
            system.view_all_students()

        elif choice == '3':
            search_choice = input("Search by Roll No (1) or Name (2)? ")
            if search_choice == '1':
                roll_no = input("Enter Roll No: ")
                system.search_student(roll_no=roll_no)
            elif search_choice == '2':
                name = input("Enter Name: ")
                system.search_student(name=name)

        elif choice == '4':
            roll_no = input("Enter Roll No of the student to update: ")
            name = input("Enter new Name (leave blank to keep unchanged): ")
            age = input("Enter new Age (leave blank to keep unchanged): ")
            course = input("Enter new Course (leave blank to keep unchanged): ")
            system.update_student(roll_no, name, age, course)

        elif choice == '5':
            roll_no = input("Enter Roll No of the student to delete: ")
            system.delete_student(roll_no)

        elif choice == '6':
            print("Exiting the system.")
            break

        else:
            print("Invalid choice. Please try again.")
