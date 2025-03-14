# CGPA-Calculator-with-C
#include <stdio.h>

void displayGradePoints() {
    printf("\nGrade Points Table:\n");
    printf("A+  = 4.0\n");
    printf("A   = 3.75\n");
    printf("A-  = 3.5\n");
    printf("B+  = 3.25\n");
    printf("B   = 3.0\n");
    printf("B-  = 2.75\n");
    printf("C+  = 2.5\n");
    printf("C   = 2.25\n");
    printf("D   = 2.0\n");
    printf("F   = 0.0\n");
}

void calculateCGPA(int numSemesters) {
    float totalGradePoints = 0, totalCredits = 0;

    for (int i = 0; i < numSemesters; i++) {
        float semesterGradePoints = 0, semesterCredits = 0;
        int choice;

        printf("\nFor semester %d:\n", i + 1);
        printf("1. Enter GPA for each subject\n");
        printf("2. Enter total credits and semester GPA\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        if (choice == 1) {
            int numSubjects;
            float gradePoints, credits;

            printf("Enter the number of subjects: ");
            scanf("%d", &numSubjects);

            displayGradePoints();

            for (int j = 0; j < numSubjects; j++) {
                do {
                    printf("Enter grade points for subject %d: ", j + 1);
                    scanf("%f", &gradePoints);
                    if (gradePoints!=4&&gradePoints!=3.75&&
                        gradePoints!=3.5
                        &&gradePoints!=3.25&&gradePoints!=3
                        &&gradePoints!=2.75&&gradePoints!=2.5
                        &&gradePoints!=2.25&&gradePoints!=2&&gradePoints!=0)
                        {
                        printf("Error: Grade points must be one of the designated values.\n");
                        }

                }
                while (gradePoints!=4&&gradePoints!=3.75&&
                       gradePoints!=3.5&&gradePoints!=3.25&&
                       gradePoints!=3&&gradePoints!=2.75&&gradePoints!=2.5&&
                       gradePoints!=2.25&&gradePoints!=2&&gradePoints!=0);


                do {
                    printf("Enter credits for subject %d: ", j + 1);
                    scanf("%f", &credits);
                    if (credits < 0) {
                        printf("Error: Credits cannot be negative.\n");
                    }
                } while (credits < 0);

                semesterGradePoints += gradePoints * credits;
                semesterCredits += credits;
            }

        }
         else if (choice == 2) {
            do {
                printf("Enter total credits for semester %d: ", i + 1);
                scanf("%f", &semesterCredits);
                if (semesterCredits < 0) {
                    printf("Error: Credits cannot be negative.\n");
                }
            } while (semesterCredits < 0);

            do {
                float semesterCGPA;
             do {
                printf("Enter GPA for semester %d: ", i + 1);
                scanf("%f", &semesterCGPA);
                if (semesterCGPA < 0 || semesterCGPA > 4) {
                    printf("Error: GPA must be between 0 and 4.\n");
                }}while (semesterCGPA < 0 || semesterCGPA > 4);
                semesterGradePoints = semesterCGPA * semesterCredits;
            } while (semesterGradePoints < 0);
        }
        else {
            printf("Invalid choice\n");
            i--; // Go back to the same semester
            continue;
        }

        totalGradePoints += semesterGradePoints;
        totalCredits += semesterCredits;
    }

    printf("\nYour overall CGPA is: %.2f\n", totalGradePoints / totalCredits);
    printf("Total credits completed: %.2f\n", totalCredits);
}

int main() {
    int choice;

    while (1) {
        printf("\nCGPA Calculator Menu:\n");
        printf("1. Calculate CGPA for multiple semesters\n");
        printf("2. Calculate GPA for a single semester\n");
        printf("3. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        if (choice == 1) {
            int numSemesters;
            printf("Enter the number of semesters: ");
            scanf("%d", &numSemesters);
            calculateCGPA(numSemesters);
        } else if (choice == 2) {
            calculateCGPA(1); // Calculate for one semester
        } else if (choice == 3) {
            printf("Exiting...\n");
            break; // Exit the loop and end the program
        } else {
            printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
}

