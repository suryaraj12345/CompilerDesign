#include <stdio.h>
#include <ctype.h>
#include <string.h>

int n;
char production[10][10], first[10][10], follow[10][10];
char non_terminals[10], terminals[10], start_symbol;
int nt_count = 0, t_count = 0;

// Function to check if a symbol is terminal
int is_terminal(char symbol) {
    return !isupper(symbol);  // if the symbol is not uppercase, it's a terminal
}

// Function to find the FIRST set of a given symbol
void find_first(char symbol, char result[]) {
    int i, j;

    // If the symbol is a terminal, return it in the result
    if (is_terminal(symbol)) {
        strncat(result, &symbol, 1);
        return;
    }

    // Otherwise, find the FIRST set for the non-terminal
    for (i = 0; i < n; i++) {
        if (production[i][0] == symbol) {
            if (is_terminal(production[i][2])) {
                strncat(result, &production[i][2], 1);
            } else {
                find_first(production[i][2], result);
            }
        }
    }
}

// Function to find the FOLLOW set of a non-terminal
void find_follow(char symbol) {
    int i, j;
    char result[10] = "";

    // Start symbol has '$' in its FOLLOW set
    if (symbol == start_symbol) {
        strcat(follow[symbol - 'A'], "$");
    }

    // Iterate through each production
    for (i = 0; i < n; i++) {
        for (j = 2; j < strlen(production[i]); j++) {
            if (production[i][j] == symbol) {
                if (j + 1 < strlen(production[i])) {
                    // If the next symbol is terminal, add it to FOLLOW set
                    if (is_terminal(production[i][j + 1])) {
                        strncat(follow[symbol - 'A'], &production[i][j + 1], 1);
                    } else {
                        // If the next symbol is a non-terminal, add its FIRST set (excluding epsilon)
                        find_first(production[i][j + 1], result);
                        for (int k = 0; k < strlen(result); k++) {
                            if (result[k] != 'e') {
                                strncat(follow[symbol - 'A'], &result[k], 1);
                            }
                        }

                        // If the non-terminal can derive epsilon, add FOLLOW of LHS
                        if (strchr(result, 'e') != NULL) {
                            find_follow(production[i][0]);
                            strcat(follow[symbol - 'A'], follow[production[i][0] - 'A']);
                        }
                    }
                } else {
                    // If at the end of production, add FOLLOW of LHS non-terminal
                    if (production[i][0] != symbol) {
                        find_follow(production[i][0]);
                        strcat(follow[symbol - 'A'], follow[production[i][0] - 'A']);
                    }
                }
            }
        }
    }
}

int main() {
    int i;
    char choice, c;

    printf("Enter the number of productions: ");
    scanf("%d", &n);

    printf("Enter the productions (e.g., E=TR, use 'e' for epsilon):\n");
    for (i = 0; i < n; i++) {
        scanf("%s", production[i]);
        if (strchr(non_terminals, production[i][0]) == NULL) {
            non_terminals[nt_count++] = production[i][0];
        }
    }

    printf("Enter the start symbol: ");
    scanf(" %c", &start_symbol);

    // Initialize follow sets
    for (i = 0; i < nt_count; i++) {
        follow[non_terminals[i] - 'A'][0] = '\0';
    }

    // Compute FOLLOW set for each non-terminal
    for (i = 0; i < nt_count; i++) {
        find_follow(non_terminals[i]);
    }

    // Print the FOLLOW sets
    printf("\nFOLLOW sets:\n");
    for (i = 0; i < nt_count; i++) {
        printf("FOLLOW(%c) = { %s }\n", non_terminals[i], follow[non_terminals[i] - 'A']);
    }

    return 0;
}
