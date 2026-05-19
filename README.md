main.c
#include <stdio.h>
#include <string.h>

#define MAX 100

// Structure definition
struct Student {
    char name[50];
    int admissionNumber;
    int age;
    float marks[3];
    float average;
    char grade;
};

// Function declarations
void calculateAverageAndGrade(struct Student *s);
void addStudent(struct Student students[], int *count);
void displayStudents(struct Student students[], int count);
void searchStudent(struct Student students[], int count);
void updateStudent(struct Student students[], int count);
void bestStudent(struct Student students[], int count);

// Function to calculate average and grade
void calculateAverageAndGrade(struct Student *s) {
    s->average = (s->marks[0] + s->marks[1] + s->marks[2]) / 3;

    if (s->average >= 70)
        s->grade = 'A';
    else if (s->average >= 60)
        s->grade = 'B';
    else if (s->average >= 50)
        s->grade = 'C';
    else if (s->average >= 40)
        s->grade = 'D';
    else
        s->grade = 'E';
}

// Function to add a student
void addStudent(struct Student students[], int *count) {
    printf("\nEnter student name: ");
    scanf(" %[^
]", students[*count].name);

    printf("Enter admission number: ");
    scanf("%d", &students[*count].admissionNumber);

    printf("Enter age: ");
    scanf("%d", &students[*count].age);

    printf("Enter marks for 3 subjects:\n");
    for (int i = 0; i < 3; i++) {
        printf("Subject %d: ", i + 1);
        scanf("%f", &students[*count].marks[i]);
    }

    calculateAverageAndGrade(&students[*count]);

    printf("Student added successfully!\n");

    (*count)++;
}

// Function to display all students
void displayStudents(struct Student students[], int count) {
    if (count == 0) {
        printf("\nNo student records found.\n");
        return;
    }

    printf("\n===== STUDENT RECORDS =====\n");

    for (int i = 0; i < count; i++) {
        printf("\nStudent %d\n", i + 1);
        printf("Name: %s\n", students[i].name);
        printf("Admission Number: %d\n", students[i].admissionNumber);
        printf("Age: %d\n", students[i].age);
        printf("Marks: %.2f %.2f %.2f\n",
               students[i].marks[0],
               students[i].marks[1],
               students[i].marks[2]);
        printf("Average: %.2f\n", students[i].average);
        printf("Grade: %c\n", students[i].grade);
    }
}

// Function to search student
void searchStudent(struct Student students[], int count) {
    int adm;
    int found = 0;

    printf("\nEnter admission number to search: ");
    scanf("%d", &adm);

    for (int i = 0; i < count; i++) {
        if (students[i].admissionNumber == adm) {
            printf("\nStudent Found!\n");
            printf("Name: %s\n", students[i].name);
            printf("Admission Number: %d\n", students[i].admissionNumber);
            printf("Age: %d\n", students[i].age);
            printf("Average: %.2f\n", students[i].average);
            printf("Grade: %c\n", students[i].grade);
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Student not found.\n");
    }
}

// Function to update student marks
void updateStudent(struct Student students[], int count) {
    int adm;
    int found = 0;

    printf("\nEnter admission number to update: ");
    scanf("%d", &adm);

    for (int i = 0; i < count; i++) {
        if (students[i].admissionNumber == adm) {
            printf("\nEnter new marks for 3 subjects:\n");

            for (int j = 0; j < 3; j++) {
                printf("Subject %d: ", j + 1);
                scanf("%f", &students[i].marks[j]);
            }

            calculateAverageAndGrade(&students[i]);

            printf("Student record updated successfully!\n");
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Student not found.\n");
    }
}

// Function to display best student
void bestStudent(struct Student students[], int count) {
    if (count == 0) {
        printf("\nNo student records available.\n");
        return;
    }

    int best = 0;

    for (int i = 1; i < count; i++) {
        if (students[i].average > students[best].average) {
            best = i;
        }
    }

    printf("\n===== BEST PERFORMING STUDENT =====\n");
    printf("Name: %s\n", students[best].name);
    printf("Admission Number: %d\n", students[best].admissionNumber);
    printf("Average: %.2f\n", students[best].average);
    printf("Grade: %c\n", students[best].grade);
}

// Main function
int main() {
    struct Student students[MAX];
    int count = 0;
    int choice;

    do {
        printf("\n===== STUDENT MANAGEMENT SYSTEM =====\n");
        printf("1. Add Student\n");
        printf("2. Display All Students\n");
        printf("3. Search Student\n");
        printf("4. Update Student\n");
        printf("5. Best Performing Student\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addStudent(students, &count);
                break;

            case 2:
                displayStudents(students, count);
                break;

            case 3:
                searchStudent(students, count);
                break;

            case 4:
                updateStudent(students, count);
                break;

            case 5:
                bestStudent(students, count);
                break;

            case 6:
                printf("Exiting program...\n");
                break;

            default:
                printf("Invalid choice. Please try again.\n");
        }

    } while (choice != 6);

    return 0;
}
