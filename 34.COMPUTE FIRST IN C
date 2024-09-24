#include <stdio.h>
#include <ctype.h>
#include <string.h>

int n;
char production[10][10], first[10];

int is_terminal(char ch) {
    return !isupper(ch);
}
void find_first(char symbol) {
    int i, j;
    if (is_terminal(symbol)) {
        printf("%c ", symbol);
        return;
    }
    
    for (i = 0; i < n; i++) {
        if (production[i][0] == symbol) {
            if (is_terminal(production[i][2])) {
                printf("%c ", production[i][2]);
            } else {
                find_first(production[i][2]);
            }
        }
    }
}

int main() {
    int i;
    char choice, c, ch;
    
    printf("Enter the number of productions: ");
    scanf("%d", &n);
    
    printf("Enter the productions (e.g., E=E+T):\n");
    for (i = 0; i < n; i++) {
        scanf("%s", production[i]);
    }
    
    do {
        printf("Find FIRST of: ");
        scanf(" %c", &c);
        
        printf("FIRST(%c) = { ", c);
        find_first(c);
        printf("}\n");
        
        printf("Do you want to continue (y/n)? ");
        scanf(" %c", &choice);
    } while (choice == 'y' || choice == 'Y');
    
    return 0;
}
