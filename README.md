# Library-Management-System-
A simple C project using linked list and file handling 
#include <stdio.h>

#include <stdlib.h>

#include <string.h>

struct Book {

int id;

char title[100];

char author[100];

int issued; 

struct Book* next;

};

struct Book* head = NULL;

struct Book* createBook(int id, char title[], char author[]) {

struct Book* newBook = (struct Book*)malloc(sizeof(struct Book));

newBook->id = id;

strcpy(newBook->title, title);

strcpy(newBook->author, author);

newBook->issued = 0;

newBook->next = NULL;

return newBook;

}

void addBook(int id, char title[], char author[]) {

struct Book* newBook = createBook(id, title, author);

newBook->next = head;

head = newBook;

printf("? Book added successfully.\n");

}

void deleteBook(int id) {

struct Book* temp = head;

struct Book* prev = NULL;



while (temp != NULL && temp->id != id) {

    prev = temp;

    temp = temp->next;

}



if (temp == NULL) {

    printf("? Book not found.\n");

    return;

}



if (prev == NULL)

    head = temp->next;

else

    prev->next = temp->next;



free(temp);

printf("? Book deleted successfully.\n");

}

void searchBook(char title[]) {

struct Book* temp = head;

int found = 0;

while (temp != NULL) {

    if (strcmp(temp->title, title) == 0) {

        printf("?? Book Found:\nID: %d\nTitle: %s\nAuthor: %s\nStatus: %s\n",

               temp->id, temp->title, temp->author,

               temp->issued ? "Issued" : "Available");

        found = 1;

        break;

    }

    temp = temp->next;

}

if (!found)

    printf("? Book not found.\n");

}

void displayBooks() {

struct Book* temp = head;

if (temp == NULL) {

    printf("?? No books available.\n");

    return;

}

printf("\n--- Book List ---\n");

while (temp != NULL) {

    printf("ID: %d | Title: %s | Author: %s | Status: %s\n",

           temp->id, temp->title, temp->author,

           temp->issued ? "Issued" : "Available");

    temp = temp->next;

}

}

void issueBook(int id) {

struct Book* temp = head;

while (temp != NULL) {

    if (temp->id == id) {

        if (temp->issued) {

            printf("? Book is already issued.\n");

        } else {

            temp->issued = 1;

            printf("? Book issued successfully.\n");

        }

        return;

    }

    temp = temp->next;

}



printf("? Book not found.\n");

}

void returnBook(int id) {

struct Book* temp = head;



while (temp != NULL) {

    if (temp->id == id) {

        if (!temp->issued) {

            printf("? Book was not issued.\n");

        } else {

            temp->issued = 0;

            printf("? Book returned successfully.\n");

        }

        return;

    }

    temp = temp->next;

}



printf("? Book not found.\n");

}

void menu() {

printf("\n--- Library Management System ---\n");

printf("1. Add Book\n");

printf("2. Delete Book\n");

printf("3. Search Book by Title\n");

printf("4. Display All Books\n");

printf("5. Issue Book\n");

printf("6. Return Book\n");

printf("7. Exit\n");

printf("Choose an option: ");

}

int main() {

int choice, id;

char title[100], author[100];

while (1) {

    menu();

    scanf("%d", &choice);

    getchar(); 

    switch (choice) {

        case 1:

            printf("Enter Book ID: ");

            scanf("%d", &id);

            getchar();

            printf("Enter Title: ");

            fgets(title, sizeof(title), stdin);

            title[strcspn(title, "\n")] = '\0';

            printf("Enter Author: ");

            fgets(author, sizeof(author), stdin);

            author[strcspn(author, "\n")] = '\0';

            addBook(id, title, author);

            break;

        case 2:

            printf("Enter Book ID to delete: ");

            scanf("%d", &id);

            deleteBook(id);

            break;

        case 3:

            printf("Enter Book Title to search: ");

            fgets(title, sizeof(title), stdin);

            title[strcspn(title, "\n")] = '\0';

            searchBook(title);

            break;

        case 4:

            displayBooks();

            break;

        case 5:

            printf("Enter Book ID to issue: ");

            scanf("%d", &id);

            issueBook(id);

            break;

        case 6:

            printf("Enter Book ID to return: ");

            scanf("%d", &id);

            returnBook(id);

            break;

        case 7:

            printf("?? Exiting... Goodbye!\n");

            exit(0);

        default:

            printf("? Invalid choice. Try again.\n");

    }

}

return 0;

}
