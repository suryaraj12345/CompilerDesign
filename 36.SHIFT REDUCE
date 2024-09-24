#include <stdio.h>
#include <string.h>

char stack[100], input[100];  
int top = -1, pos = 0;      

void push(char c) {
    stack[++top] = c;
}
void pop() {
    stack[top--] = '\0';
}
void display() {
    printf("Stack: %s\t Input: %s\n", stack, input + pos);
}
int reduce() {
    if (top >= 2 && stack[top] == 'E' && stack[top - 1] == '+' && stack[top - 2] == 'E') {
        printf("Reducing by E -> E + E\n");
        pop(); pop(); pop();
        push('E');
        return 1;
    } else if (top >= 2 && stack[top] == 'E' && stack[top - 1] == '*' && stack[top - 2] == 'E') {
        printf("Reducing by E -> E * E\n");
        pop(); pop(); pop();
        push('E');
        return 1;
    } else if (top >= 0 && stack[top] == 'id') {
        printf("Reducing by E -> id\n");
        pop();
        push('E');
        return 1;
    }
    return 0;
}
void shift_reduce_parse() {
    printf("\nParsing process:\n");
    while (pos < strlen(input)) {
        printf("Shifting %c to the stack\n", input[pos]);
        push(input[pos]);
        pos++;
        display();
        while (reduce()) {
            display();
        }
    }
    if (top == 0 && stack[0] == 'E') {
        printf("\nInput successfully parsed as valid expression!\n");
    } else {
        printf("\nError: Unable to parse the input\n");
    }
}

int main() {
    printf("Enter the input expression (e.g., id+id*id): ");
    scanf("%s", input);
    shift_reduce_parse();

    return 0;
}
