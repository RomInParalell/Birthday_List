# Birthday_List
Birthday list is about storing the data of the user birthday and display it on when it's their birthday (using C)



This is the source code : 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_PERSONS 100

struct Person {
    char name[50];
    int day;
    int month;
    int year;
};

struct Person birthdayList[MAX_PERSONS];
int numPersons = 0;
//#####################################################################
void addPerson() {
    struct Person person;
    FILE* save = fopen("save.txt", "a");
    printf("\nEnter name: ");
    scanf("%s", person.name);
    printf("Enter day (1-31): ");
    scanf("%d", &person.day);
    printf("Enter month (1-12): ");
    scanf("%d", &person.month);
    printf("Enter year: ");
    scanf("%d", &person.year);
    birthdayList[numPersons++] = person;
    fprintf(save,"%s : %d/%d/%d\n",person.name,person.day,person.month,person.year);
    fprintf(save,"###############");
    fclose(save);
}
//#####################################################################
void editPerson() {
    char name[50];
    printf("\nEnter name to edit: ");
    scanf("%s", name);

    int index = -1;
    for (int i = 0; i < numPersons; i++) {
        if (strcmp(birthdayList[i].name, name) == 0) {
            index = i;
            break;
        }
    }

    if (index == -1) {
        printf("Person not found.\n");
        return;
    }

    printf("Enter new day (1-31): ");
    scanf("%d", &birthdayList[index].day);
    printf("Enter new month (1-12): ");
    scanf("%d", &birthdayList[index].month);
    printf("Enter new year: ");
    scanf("%d", &birthdayList[index].year);

    printf("Person updated.\n");
}
//#####################################################################
void displayList() {
    printf("\nBirthday List:\n");
    for (int i = 0; i < numPersons; i++) {
        printf("%s - %d/%d/%d\n", birthdayList[i].name, birthdayList[i].day, birthdayList[i].month, birthdayList[i].year);
    }
}
//#####################################################################
void searchPerson() {
    char name[50];
    printf("\nEnter name to search: ");
    scanf("%s", name);

    int index = -1;
    for (int i = 0; i < numPersons; i++) {
        if (strcmp(birthdayList[i].name, name) == 0) {
            index = i;
            break;
        }
    }

    if (index == -1) {
        printf("Person not found.\n");
        return;
    }

    printf("%s's birthday is on %d/%d/%d\n", birthdayList[index].name, birthdayList[index].day, birthdayList[index].month, birthdayList[index].year);
}
//#####################################################################
void displayComingBirthdays() {
    int month;
    printf("\nEnter month (1-12): ");
    scanf("%s", &month);

    printf("\nBirthdays in month %s:\n", month);
    for (int i = 0; i < numPersons; i++) {
        if (birthdayList[i].month == month) {
            printf("%s - %d/%d/%d\n", birthdayList[i].name, birthdayList[i].day, birthdayList[i].month, birthdayList[i].year);
        }
    }
}
//#####################################################################
int main() {
    int choice;

    do {
        printf("\n1. Add person\n");
        printf("2. Edit person\n");
        printf("3. Display list\n");
        printf("4. Search person\n");
        printf("5. Display coming birthdays\n");
        printf("6. Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);
        getchar(); 

        switch (choice) {
            case 1:
                addPerson();
                break;
            case 2:
                editPerson();
                break;
            case 3:
                displayList();
                break;
            case 4:
                searchPerson();
                break;
            case 5:
                displayComingBirthdays();
                break;
            case 6:
                printf("\nExiting program...\n");
                break;
            default:
                printf("\nInvalid choice.\n");
        }
        printf("\n");
    } while (choice != 6);

    return 0;
}
