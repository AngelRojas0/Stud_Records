#include <iostream>
#include <string>
using namespace std;

// Maximum number of students
const int MAX_STUDENTS = 100;

// Define the Student structure
struct Student {
    int id;
    string firstName;
    string lastName;
    string course;
    float gpa;
};

Student students[MAX_STUDENTS];
int studentCount = 0;

// Function to display the menu
void displayMenu() {
    cout << "---- MENU ----" << endl;
    cout << "[1] Add Student" << endl;
    cout << "[2] Edit Student" << endl;
    cout << "[3] Delete Student" << endl;
    cout << "[4] View All Students" << endl;
    cout << "[5] Exit Program" << endl;
}

// Function to add a student
void addStudent() {
    if (studentCount >= MAX_STUDENTS) {
        cout << "Student record is full!" << endl;
        return;
    }

    Student newStudent;
    cout << "Enter Student ID: ";
    cin >> newStudent.id;
    cout << "Enter First Name: ";
    cin >> newStudent.firstName;
    cout << "Enter Last Name: ";
    cin >> newStudent.lastName;
    cout << "Enter Course: ";
    cin >> newStudent.course;
    cout << "Enter GPA: ";
    cin >> newStudent.gpa;

    students[studentCount++] = newStudent;
    cout << "Student added successfully!" << endl;
}

// Function to edit a student's data
void editStudent() {
    system ("cls");
    int id;
    cout << "Enter Student ID to edit: ";
    cin >> id;

    for (int i = 0; i < studentCount; ++i) {
        if (students[i].id == id) {
            cout << "Enter new First Name: ";
            cin >> students[i].firstName;
            cout << "Enter new Last Name: ";
            cin >> students[i].lastName;
            cout << "Enter new Course: ";
            cin >> students[i].course;
            cout << "Enter new GPA: ";
            cin >> students[i].gpa;
            cout << "Student data updated successfully!" << endl;
            return;
        }
    }
    cout << "Student ID not found!" << endl;
}

// Function to delete a student record
void deleteStudent() {
    int id;
    cout << "Enter Student ID to delete: ";
    cin >> id;

    for (int i = 0; i < studentCount; ++i) {
        if (students[i].id == id) {
            for (int j = i; j < studentCount - 1; ++j) {
                students[j] = students[j + 1];
            }
            --studentCount;
            cout << "Student deleted successfully!" << endl;
            return;
        }
    }
    cout << "Student ID not found!" << endl;
}

// Function to view all students
void viewAllStudents() {
    if (studentCount == 0) {
        cout << "No student records available!" << endl;
        return;
    }

    cout << "--- STUDENT RECORDS ---" << endl;
    for (int i = 0; i < studentCount; ++i) {
        cout << "\nID: " << students[i].id
             << "\nName: " << students[i].firstName << " " << students[i].lastName
             << "\nCourse: " << students[i].course
             << "\nGPA: " << students[i].gpa << endl;
    }
}

int main() {
    int choice;

    do {
        displayMenu();
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            addStudent();
            break;
        case 2:
            editStudent();
            break;
        case 3:
            deleteStudent();
            break;
        case 4:
            viewAllStudents();
            break;
        case 5:
            cout << "Exiting program..." << endl;
            break;
        default:
            cout << "Invalid choice! Please try again." << endl;
        }
    } while (choice != 5);

    return 0;
}
