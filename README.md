// Program A: STUDENTS (1D array) - input, display, search
#include <stdio.h>

int main() {
    int N;
    printf("Enter number of students: ");
    scanf("%d", &N);
    int STUDENTS[N];

    for (int i = 0; i < N; i++) {
        printf("Enter roll number for student %d: ", i+1);
        scanf("%d", &STUDENTS[i]);
    }

    printf("\nRoll numbers:\n");
    for (int i = 0; i < N; i++) printf("%d ", STUDENTS[i]);
    printf("\n");

    int key, found = 0;
    printf("\nEnter roll number to search: ");
    scanf("%d", &key);
    for (int i = 0; i < N; i++) {
        if (STUDENTS[i] == key) { found = 1; printf("Found at position %d (index %d)\n", i+1, i); break; }
    }
    if (!found) printf("Roll number %d not found.\n", key);
    return 0;
}









// Program B: MARKS (1D array) - input, sort descending, display
#include <stdio.h>

int main() {
    int N;
    printf("Enter number of students: ");
    scanf("%d", &N);
    int MARKS[N];

    for (int i = 0; i < N; i++) {
        printf("Enter marks for student %d: ", i+1);
        scanf("%d", &MARKS[i]);
    }

    // simple selection sort descending
    for (int i = 0; i < N-1; i++) {
        int mx = i;
        for (int j = i+1; j < N; j++)
            if (MARKS[j] > MARKS[mx]) mx = j;
        if (mx != i) { int t = MARKS[i]; MARKS[i] = MARKS[mx]; MARKS[mx] = t; }
    }

    printf("\nMarks sorted in descending order:\n");
    for (int i = 0; i < N; i++) printf("%d ", MARKS[i]);
    printf("\n");
    return 0;
}






// Program C: STUDENTS_MARK (2 x N) - make from STUDENTS and MARKS, display
#include <stdio.h>

int main() {
    int N;
    printf("Enter number of students: ");
    scanf("%d", &N);
    int STUDENTS[N], MARKS[N], STUDENTS_MARK[2][N];

    printf("Enter roll numbers:\n");
    for (int i = 0; i < N; i++) scanf("%d", &STUDENTS[i]);
    printf("Enter marks:\n");
    for (int i = 0; i < N; i++) scanf("%d", &MARKS[i]);

    // assign into 2xN array
    for (int j = 0; j < N; j++) {
        STUDENTS_MARK[0][j] = STUDENTS[j]; // row 0 = roll
        STUDENTS_MARK[1][j] = MARKS[j];    // row 1 = mark
    }

    printf("\nSTUDENTS_MARK (2 x %d):\n", N);
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < N; j++) printf("%d\t", STUDENTS_MARK[i][j]);
        printf("\n");
    }
    return 0;
}







// Program D: STUDENTS_MARKS (4 x N) - row0:roll, row1..3:marks of 3 subjects
#include <stdio.h>

int main() {
    int N;
    printf("Enter number of students: ");
    scanf("%d", &N);
    int STUDENTS_MARKS[4][N];

    printf("Enter roll numbers (row 0):\n");
    for (int j = 0; j < N; j++) scanf("%d", &STUDENTS_MARKS[0][j]);

    for (int subj = 1; subj <= 3; subj++) {
        printf("Enter marks for subject %d:\n", subj);
        for (int j = 0; j < N; j++) scanf("%d", &STUDENTS_MARKS[subj][j]);
    }

    printf("\nSTUDENTS_MARKS (4 x %d):\n", N);
    for (int i = 0; i < 4; i++) {
        for (int j = 0; j < N; j++) printf("%d\t", STUDENTS_MARKS[i][j]);
        printf("\n");
    }
    return 0;
}






// Program E: STUDENTS_NAMES - input and display string array of names
#include <stdio.h>
#include <string.h>

int main() {
    int N;
    printf("Enter number of students: ");
    scanf("%d", &N);
    char STUDENTS_NAMES[N][50];

    for (int i = 0; i < N; i++) {
        printf("Enter name of student %d: ", i+1);
        scanf("%s", STUDENTS_NAMES[i]); // reads single token name
    }

    printf("\nStudent names:\n");
    for (int i = 0; i < N; i++) printf("%s\n", STUDENTS_NAMES[i]);
    return 0;
}








// Program F: STUDENTS_NAMES_SORTED - copy and sort names alphabetically (uses strcpy)
#include <stdio.h>
#include <string.h>

int main() {
    int N;
    printf("Enter number of students: ");
    scanf("%d", &N);
    char STUDENTS_NAMES[N][50], STUDENTS_NAMES_SORTED[N][50], tmp[50];

    for (int i = 0; i < N; i++) {
        printf("Enter name %d: ", i+1);
        scanf("%s", STUDENTS_NAMES[i]);
        strcpy(STUDENTS_NAMES_SORTED[i], STUDENTS_NAMES[i]); // copy
    }

    // sort copy
    for (int i = 0; i < N-1; i++) {
        for (int j = i+1; j < N; j++) {
            if (strcmp(STUDENTS_NAMES_SORTED[i], STUDENTS_NAMES_SORTED[j]) > 0) {
                strcpy(tmp, STUDENTS_NAMES_SORTED[i]);
                strcpy(STUDENTS_NAMES_SORTED[i], STUDENTS_NAMES_SORTED[j]);
                strcpy(STUDENTS_NAMES_SORTED[j], tmp);
            }
        }
    }

    printf("\nOriginal names:\n");
    for (int i = 0; i < N; i++) printf("%s\n", STUDENTS_NAMES[i]);

    printf("\nSorted names (STUDENTS_NAMES_SORTED):\n");
    for (int i = 0; i < N; i++) printf("%s\n", STUDENTS_NAMES_SORTED[i]);

    return 0;
}






// Program G: Calculate_Average - computes average of 3 subject marks from STUDENTS_MARKS (4xN)
#include <stdio.h>

void Calculate_Average(int STUDENTS_MARKS[4][100], int N, float AVERAGE[]) {
    for (int j = 0; j < N; j++) {
        int sum = 0;
        for (int i = 1; i <= 3; i++) sum += STUDENTS_MARKS[i][j];
        AVERAGE[j] = sum / 3.0f;
    }
}

int main() {
    int N;
    printf("Enter number of students: ");
    scanf("%d", &N);
    int STUDENTS_MARKS[4][100];
    float AVERAGE[N];

    printf("Enter roll numbers (row 0):\n");
    for (int j = 0; j < N; j++) scanf("%d", &STUDENTS_MARKS[0][j]);

    for (int subj = 1; subj <= 3; subj++) {
        printf("Enter marks for subject %d:\n", subj);
        for (int j = 0; j < N; j++) scanf("%d", &STUDENTS_MARKS[subj][j]);
    }

    Calculate_Average(STUDENTS_MARKS, N, AVERAGE);

    printf("\nAVERAGE of each student:\n");
    for (int j = 0; j < N; j++)
        printf("Roll %d -> %.2f\n", STUDENTS_MARKS[0][j], AVERAGE[j]);

    return 0;
}







// Program H: Find_Topper - find student with maximum average and print their name
#include <stdio.h>
#include <string.h>

void Find_Topper(float AVERAGE[], int N, char STUDENTS_NAMES[][50]) {
    int idx = 0;
    for (int i = 1; i < N; i++)
        if (AVERAGE[i] > AVERAGE[idx]) idx = i;
    printf("The topper is : %s (average = %.2f)\n", STUDENTS_NAMES[idx], AVERAGE[idx]);
}

int main() {
    int N;
    printf("Enter number of students: ");
    scanf("%d", &N);
    float AVERAGE[N];
    char STUDENTS_NAMES[N][50];

    for (int i = 0; i < N; i++) {
        printf("Enter name of student %d: ", i+1);
        scanf("%s", STUDENTS_NAMES[i]);
        printf("Enter average marks of %s: ", STUDENTS_NAMES[i]);
        scanf("%f", &AVERAGE[i]);
    }

    Find_Topper(AVERAGE, N, STUDENTS_NAMES);
    return 0;
}

