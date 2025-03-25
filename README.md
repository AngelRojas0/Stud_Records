#include <iostream>
#include <string>
using namespace std;

const int MAX_STUDENTS = 100;
 
struct Student {
    int id;
    string firstName;
    string lastName;
    string course;
    double gpa;
};

Student students[MAX_STUDENTS];
int studentCount = 0;
void displayMenu() {
    cout << "---- MENU ----" << endl;
    cout << "[1] Add Student" << endl;
    cout << "[2] Edit Student" << endl;
    cout << "[3] Delete Student" << endl;
    cout << "[4] View All Students" << endl;
    cout << "[5] Sort and View Students" << endl;
    cout << "[6] Exit Program" << endl;
}

void addStudent() {
    if (studentCount >= MAX_STUDENTS) {
        cout << "Student record is full!" << endl;
        return;
    }

    Student newStudent;
    cout << "Enter Student ID: ";
    cin >> newStudent.id;

    cin.ignore(); 
    cout << "Enter First Name: ";
    getline(cin, newStudent.firstName);

    cout << "Enter Last Name: ";
    getline(cin, newStudent.lastName);

    cout << "Enter Course: ";
    getline(cin, newStudent.course);

    cout << "Enter GPA: ";
    cin >> newStudent.gpa;

    cin.ignore(); 
    students[studentCount++] = newStudent;
    cout << "Student added successfully!" << endl;
}

void editStudent() {
    int id;
    cout << "Enter Student ID to edit: ";
    cin >> id;

    for (int i = 0; i < studentCount; ++i) {
        if (students[i].id == id) {
            cout << "Enter new First Name: ";
            cin >> students[i].firstName;
            cin.ignore();
            cout << "Enter new Last Name: ";
            cin >> students[i].lastName;
            cin.ignore();
            cout << "Enter new Course: ";
            cin >> students[i].course;
            cin.ignore();
            cout << "Enter new GPA: ";
            cin >> students[i].gpa;
            cin.ignore();
            cout << "Student data updated successfully!" << endl;
            return;
        }
    }
    cout << "Student ID not found!" << endl;
}

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

void sortByName() {
    for (int i = 0; i < studentCount - 1; ++i) {
        for (int j = 0; j < studentCount - i - 1; ++j) {
            if (students[j].lastName > students[j + 1].lastName ||
                (students[j].lastName == students[j + 1].lastName && students[j].firstName > students[j + 1].firstName)) {
                swap(students[j], students[j + 1]);
            }
        }
    }
}

void sortByGPA() {
    for (int i = 0; i < studentCount - 1; ++i) {
        for (int j = 0; j < studentCount - i - 1; ++j) {
            if (students[j].gpa < students[j + 1].gpa) {
                swap(students[j], students[j + 1]);
            }
        }
    }
}

void sortAndViewStudents() {
    if (studentCount == 0) {
        cout << "No student records available!" << endl;
        return;
    }

    int sortOption;
    cout << "Sort by: [1] Alphabetical Order [2] GPA: ";
    cin >> sortOption;

    if (sortOption == 1) {
        sortByName();
        cout << "Sorted by Alphabetical Order:" << endl;
    } else if (sortOption == 2) {
        sortByGPA();
        cout << "Sorted by GPA:" << endl;
    } else {
        cout << "Invalid option!" << endl;
        return;
    }

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
        system("CLS"); 
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
            sortAndViewStudents();
            break;
        case 6:
            cout << "Exiting program..." << endl;
            break;
        default:
            cout << "Invalid choice! Please try again." << endl;
        }
        if (choice != 6) {
            cout << "\nPress Enter to continue...";
            cin.ignore(); 
            cin.get();    
        }

    } while (choice != 6);

    return 0;
}
