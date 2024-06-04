#include <stdio.h>
#include <stdlib.h>

struct book {
    char title[50];
    char author[50];
    int year;
    int copies;
};

struct book *books[100];
int num_books = 0;

void add_book() {
    struct book *book = malloc(sizeof(struct book));

    printf("Enter the title of the book: ");
    scanf("%s", book->title);

    printf("Enter the author of the book: ");
    scanf("%s", book->author);

    printf("Enter the year of publication: ");
    scanf("%d", &book->year);

    printf("Enter the number of copies: ");
    scanf("%d", &book->copies);

    books[num_books++] = book;
}

void list_books() {
    for (int i = 0; i < num_books; i++) {
        printf("%s by %s (%d)\n", books[i]->title, books[i]->author, books[i]->year);
    }
}

void search_book() {
    char title[50];

    printf("Enter the title of the book you want to search for: ");
    scanf("%s", title);

    for (int i = 0; i < num_books; i++) {
        if (strcmp(books[i]->title, title) == 0) {
            printf("The book is available.\n");
            return;
        }
    }

    printf("The book is not available.\n");
}

void issue_book() {
    char title[50];

    printf("Enter the title of the book you want to issue: ");
    scanf("%s", title);

    for (int i = 0; i < num_books; i++) {
        if (strcmp(books[i]->title, title) == 0) {
            if (books[i]->copies > 0) {
                books[i]->copies--;
                printf("The book has been issued.\n");
                return;
            } else {
                printf("The book is not available.\n");
                return;
            }
        }
    }

    printf("The book is not available.\n");
}

void return_book() {
    char title[50];

    printf("Enter the title of the book you want to return: ");
    scanf("%s", title);

    for (int i = 0; i < num_books; i++) {
        if (strcmp(books[i]->title, title) == 0) {
            books[i]->copies++;
            printf("The book has been returned.\n");
            return;
        }
    }

    printf("The book is not available.\n");
}

int main() {
    int choice;

    while (1) {
        printf("1. Add book\n");
        printf("2. List books\n");
        printf("3. Search book\n");
        printf("4. Issue book\n");
        printf("5. Return book\n");
        printf("6. Exit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                add_book();
                break;
            case 2:
                list_books();
                break;
            case 3:
                search_book();
                break;
            case 4:
                issue_book();
                break;
            case 5:
                return_book();
                break;
            case 6:
                exit(0);
            default:
                printf("Invalid choice.\n");
        }
    }

    return 0;
}
