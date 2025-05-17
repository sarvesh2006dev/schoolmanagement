#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX 100

struct Student {
    int rollNo;
    char firstName[50];
    char course[50];
};

struct Student students[MAX];
int count = 0;

void addStudent() {
    if (count >= MAX) {
        printf("Maximum student limit reached.\n");
        return;
    }

    printf("Enter Roll Number: ");
    scanf("%d", &students[count].rollNo);

    printf("Enter First Name: ");
    scanf("%s", students[count].firstName);

    printf("Enter Course: ");
    scanf("%s", students[count].course);

    count++;
    printf("Student added successfully.\n");
}

void findByRollNo() {
    int roll;
    printf("Enter Roll Number to search: ");
    scanf("%d", &roll);

    for (int i = 0; i < count; i++) {
        if (students[i].rollNo == roll) {
            printf("Student Found: %d %s %s\n", students[i].rollNo, students[i].firstName, students[i].course);
            return;
        }
    }
    printf("Student with Roll No %d not found.\n", roll);
}

void findByFirstName() {
    char name[50];
    printf("Enter First Name to search: ");
    scanf("%s", name);

    int found = 0;
    for (int i = 0; i < count; i++) {
        if (strcmp(students[i].firstName, name) == 0) {
            printf("Student Found: %d %s %s\n", students[i].rollNo, students[i].firstName, students[i].course);
            found = 1;
        }
    }
    if (!found)
        printf("No student found with the first name %s.\n", name);
}

void findByCourse() {
    char course[50];
    printf("Enter Course to search: ");
    scanf("%s", course);

    int found = 0;
    for (int i = 0; i < count; i++) {
        if (strcmp(students[i].course, course) == 0) {
            printf("Student: %d %s %s\n", students[i].rollNo, students[i].firstName, students[i].course);
            found = 1;
        }
    }
    if (!found)
        printf("No students found in course %s.\n", course);
}

void countStudents() {
    printf("Total number of students: %d\n", count);
}

void deleteStudent() {
    int roll;
    printf("Enter Roll Number to delete: ");
    scanf("%d", &roll);

    for (int i = 0; i < count; i++) {
        if (students[i].rollNo == roll) {
            for (int j = i; j < count - 1; j++) {
                students[j] = students[j + 1];
            }
            count--;
            printf("Student deleted successfully.\n");
            return;
        }
    }
    printf("Student with Roll No %d not found.\n", roll);
}

void updateStudent() {
    int roll;
    printf("Enter Roll Number to update: ");
    scanf("%d", &roll);

    for (int i = 0; i < count; i++) {
        if (students[i].rollNo == roll) {
            printf("Enter new First Name: ");
            scanf("%s", students[i].firstName);

            printf("Enter new Course: ");
            scanf("%s", students[i].course);

            printf("Student details updated.\n");
            return;
        }
    }
    printf("Student with Roll No %d not found.\n", roll);
}

void displayMenu() {
    printf("\n===== School Management System =====\n");
    printf("1. Add Student\n");
    printf("2. Find Student by Roll Number\n");
    printf("3. Find Student by First Name\n");
    printf("4. Find Students by Course\n");
    printf("5. Count of Students\n");
    printf("6. Delete a Student\n");
    printf("7. Update Student\n");
    printf("8. Exit\n");
    printf("Choose an option: ");
}

int main() {
    int choice;
    do {
        displayMenu();
        scanf("%d", &choice);

        switch (choice) {
        case 1: addStudent(); break;
        case 2: findByRollNo(); break;
        case 3: findByFirstName(); break;
        case 4: findByCourse(); break;
        case 5: countStudents(); break;
        case 6: deleteStudent(); break;
        case 7: updateStudent(); break;
        case 8: printf("Exiting program.\n"); break;
        default: printf("Invalid choice. Try again.\n");
        }

    } while (choice != 8);

    return 0;
}