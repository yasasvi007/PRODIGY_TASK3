# PRODIGY_TASK3

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_CONTACTS 100
#define NAME_LENGTH 50
#define PHONE_LENGTH 15
#define EMAIL_LENGTH 50

typedef struct {
    char name[NAME_LENGTH];
    char phone[PHONE_LENGTH];
    char email[EMAIL_LENGTH];
} Contact;

void addContact(Contact contacts[], int *count);
void viewContacts(Contact contacts[], int count);
void editContact(Contact contacts[], int count);
void deleteContact(Contact contacts[], int *count);

int main() {
    Contact contacts[MAX_CONTACTS];
    int count = 0;
    int choice;

    while (1) {
        printf("\nContact Management System\n");
        printf("1. Add Contact\n");
        printf("2. View Contacts\n");
        printf("3. Edit Contact\n");
        printf("4. Delete Contact\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addContact(contacts, &count);
                break;
            case 2:
                viewContacts(contacts, count);
                break;
            case 3:
                editContact(contacts, count);
                break;
            case 4:
                deleteContact(contacts, &count);
                break;
            case 5:
                exit(0);
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
}

void addContact(Contact contacts[], int *count) {
    if (*count >= MAX_CONTACTS) {
        printf("Contact list is full.\n");
        return;
    }

    printf("Enter name: ");
    scanf("%s", contacts[*count].name);
    printf("Enter phone number: ");
    scanf("%s", contacts[*count].phone);
    printf("Enter email address: ");
    scanf("%s", contacts[*count].email);

    (*count)++;
    printf("Contact added successfully.\n");
}

void viewContacts(Contact contacts[], int count) {
    if (count == 0) {
        printf("No contacts to display.\n");
        return;
    }

    for (int i = 0; i < count; i++) {
        printf("\nContact %d\n", i + 1);
        printf("Name: %s\n", contacts[i].name);
        printf("Phone: %s\n", contacts[i].phone);
        printf("Email: %s\n", contacts[i].email);
    }
}

void editContact(Contact contacts[], int count) {
    if (count == 0) {
        printf("No contacts to edit.\n");
        return;
    }

    int index;
    printf("Enter the contact number to edit (1-%d): ", count);
    scanf("%d", &index);

    if (index < 1 || index > count) {
        printf("Invalid contact number.\n");
        return;
    }

    index--; // Convert to zero-based index
    printf("Editing contact %d\n", index + 1);
    printf("Enter new name (current: %s): ", contacts[index].name);
    scanf("%s", contacts[index].name);
    printf("Enter new phone number (current: %s): ", contacts[index].phone);
    scanf("%s", contacts[index].phone);
    printf("Enter new email address (current: %s): ", contacts[index].email);
    scanf("%s", contacts[index].email);

    printf("Contact updated successfully.\n");
}

void deleteContact(Contact contacts[], int *count) {
    if (*count == 0) {
        printf("No contacts to delete.\n");
        return;
    }

    int index;
    printf("Enter the contact number to delete (1-%d): ", *count);
    scanf("%d", &index);

    if (index < 1 || index > *count) {
        printf("Invalid contact number.\n");
        return;
    }

    index--; // Convert to zero-based index

    // Shift all contacts after the deleted one to the left
    for (int i = index; i < *count - 1; i++) {
        contacts[i] = contacts[i + 1];
    }

    (*count)--;
    printf("Contact deleted successfully.\n");
}
