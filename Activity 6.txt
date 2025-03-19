#include <iostream>
using namespace std;

const int MAX_STUDENTS = 1000;
struct Student {
    int id;
    string firstname;
    string lastname;
    float gpa;
    string course;
};

Student students[MAX_STUDENTS];
int studentCount = 0;

bool isDuplicate(int studentId) {
    for (int i = 0; i < studentCount; i++) {
        if (students[i].id == studentId) {
            return true;
        }
    }
    return false;
}

void addStudent() {
    system("cls");
    if (studentCount >= MAX_STUDENTS) {
        cout << "Student limit reached.\n";
        return;
    }
    int studentId;
    cout << "Enter Student ID: ";
    cin >> studentId;

    if (isDuplicate(studentId)) {
        cout << "Student ID already exists.\n";
        return;
    }

    students[studentCount].id = studentId;
    cin.ignore();
    cout << "Enter First Name: ";
    getline(cin, students[studentCount].firstname);

    cout << "Enter Last Name: ";
    getline(cin, students[studentCount].lastname);

    cout << "Enter GPA: ";
    cin >> students[studentCount].gpa;
    cin.ignore();

    cout << "Enter Course: ";
    getline(cin, students[studentCount].course);

    studentCount++;
    cout << "Student added successfully.\n";
}

void editStudent() {
    system("cls");
    if (studentCount == 0) {
        cout << "No students available to edit.\n";
        return;
    }

    int studentId;
    cout << "Enter Student ID to edit: ";
    cin >> studentId;

    for (int i = 0; i < studentCount; i++) {
        if (students[i].id == studentId) {
            cout << "Current Student Data:\n";
            cout << "ID: " << students[i].id << "\n";
            cout << "First Name: " << students[i].firstname << "\n";
            cout << "Last Name: " << students[i].lastname << "\n";
            cout << "GPA: " << students[i].gpa << "\n";
            cout << "Course: " << students[i].course << "\n";

            cout << "Editing student data.\n";
            cin.ignore();
            cout << "Enter First Name: ";
            getline(cin, students[i].firstname);

            cout << "Enter Last Name: ";
            getline(cin, students[i].lastname);

            cout << "Enter GPA: ";
            cin >> students[i].gpa;
            cin.ignore();
            cout << "Enter Course: ";
            getline(cin, students[i].course);

            cout << "Student data updated successfully.\n";
            return;
        }
    }
    cout << "Student ID not found.\n";
}


void deleteStudent() {
    system("cls");
    if (studentCount == 0) {
        cout << "No students available to delete.\n";
        return;
    }

    int studentId;
    cout << "Enter Student ID to delete: ";
    cin >> studentId;

    bool studentFound = false;

    for (int i = 0; i < studentCount; i++) {
        if (students[i].id == studentId) {
            studentFound = true;
            cout << "Student Data Found:\n";
            cout << "ID: " << students[i].id << "\n";
            cout << "First Name: " << students[i].firstname << "\n";
            cout << "Last Name: " << students[i].lastname << "\n";
            cout << "GPA: " << students[i].gpa << "\n";
            cout << "Course: " << students[i].course << "\n";

            char confirm;
            cout << "Are you sure you want to delete this student? (y/n): ";
            cin >> confirm;

            if (confirm == 'y' || confirm == 'Y') {
                for (int j = i; j < studentCount - 1; j++) {
                    students[j] = students[j + 1];
                }
                studentCount--;
                cout << "Student deleted successfully!\n";
            } else {
                cout << "Deletion canceled.\n";
            }
            break;
        }
    }

    if (!studentFound) {
        cout << "Student ID not found.\n";
    }
}


void viewStudentsAlphabetically() {
    system("cls");
    if (studentCount == 0) {
        cout << "No students available to display.\n";
        return;
    }

    for (int i = 0; i < studentCount - 1; i++) {
        for (int j = i + 1; j < studentCount; j++) {
            if (students[i].lastname > students[j].lastname) {
                swap(students[i], students[j]);
            }
        }
    }

    cout << "Student List (Alphabetically by Last Name):\n";
    for (int i = 0; i < studentCount; i++) {
        cout << students[i].id << " | " << students[i].firstname << " | " << students[i].lastname << " | " << students[i].gpa << " | " << students[i].course << endl;
    }
}

void viewStudentsByGPA() {
    system("cls");
    if (studentCount == 0) {
        cout << "No students available to display.\n";
        return;
    }

    for (int i = 0; i < studentCount - 1; i++) {
        for (int j = i + 1; j < studentCount; j++) {
            if (students[i].gpa > students[j].gpa) {
                swap(students[i], students[j]);
            }
        }
    }

    cout << "Student List (Sorted by GPA Ascending):\n";
    for (int i = 0; i < studentCount; i++) {
        cout << students[i].id << " | " << students[i].firstname << " | " << students[i].lastname << " | " << students[i].gpa << " | " << students[i].course << endl;
    }
}

void viewStudents() {
    system("cls");
    if (studentCount == 0) {
        cout << "No students available to display.\n";
        return;
    }

    int choice;
    cout << "1. Alphabetically by Last Name\n2. View by GPA (Ascending)\nEnter your choice: ";
    cin >> choice;

    if (choice == 1) {
        viewStudentsAlphabetically();
    } else if (choice == 2) {
        viewStudentsByGPA();
    } else {
        cout << "Invalid choice.\n";
    }
}

int main() {
    int choice = 0;
    while (choice != 5) {
        system("cls");
        cout << "\n1. Add Student\n2. Edit Student\n3. Delete Student\n4. View Students\n5. Exit\nEnter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: addStudent();
            break;
            case 2: editStudent();
            break;
            case 3: deleteStudent();
            break;
            case 4: viewStudents();
            break;
            case 5: cout << "Exiting program.\n";
            break;
            default: cout << "Invalid option. Please enter a number between 1 and 5.\n";
        }
    }
    return 0;
}
