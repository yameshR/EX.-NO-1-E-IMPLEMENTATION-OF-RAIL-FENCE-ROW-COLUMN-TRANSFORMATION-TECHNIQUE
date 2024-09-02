# EX.-NO-1-E-IMPLEMENTATION-OF-RAIL-FENCE-ROW-COLUMN-TRANSFORMATION-TECHNIQUE

## AIM:
  To write a C program to implement the rail fence transposition technique.
  
## ALGORITHM:

STEP-1: Read the Plain text.

STEP-2: Arrange the plain text in row columnar matrix format.

STEP-3: Now read the keyword depending on the number of columns of the plain text.

STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.

STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

## PROGRAM:
```
#include <stdio.h>
#include <string.h>

void encrypt(char *text, int key, char *result) {
    int len = strlen(text);
    char rail[key][len];
    int i, j;
    
    // Initializing the rail matrix with '\n'
    for (i = 0; i < key; i++)
        for (j = 0; j < len; j++)
            rail[i][j] = '\n';

    int dir_down = 0;
    int row = 0, col = 0;

    // Placing the characters in the rail matrix
    for (i = 0; i < len; i++) {
        if (row == 0 || row == key - 1)
            dir_down = !dir_down;
        rail[row][col++] = text[i];
        row = dir_down ? row + 1 : row - 1;
    }

    // Constructing the result from the rail matrix
    int index = 0;
    for (i = 0; i < key; i++)
        for (j = 0; j < len; j++)
            if (rail[i][j] != '\n')
                result[index++] = rail[i][j];
    result[index] = '\0';  // Null-terminate the result string
}

void decrypt(char *cipher, int key, char *result) {
    int len = strlen(cipher);
    char rail[key][len];
    int i, j;

    // Initializing the rail matrix with '\n'
    for (i = 0; i < key; i++)
        for (j = 0; j < len; j++)
            rail[i][j] = '\n';

    int dir_down;
    int row = 0, col = 0;

    // Marking the positions with '*'
    for (i = 0; i < len; i++) {
        if (row == 0)
            dir_down = 1;
        if (row == key - 1)
            dir_down = 0;
        rail[row][col++] = '*';
        row = dir_down ? row + 1 : row - 1;
    }

    // Placing the cipher text in the marked positions
    int index = 0;
    for (i = 0; i < key; i++)
        for (j = 0; j < len; j++)
            if (rail[i][j] == '*' && index < len)
                rail[i][j] = cipher[index++];

    // Constructing the result from the rail matrix
    row = 0, col = 0;
    for (i = 0; i < len; i++) {
        if (row == 0)
            dir_down = 1;
        if (row == key - 1)
            dir_down = 0;
        if (rail[row][col] != '*')
            result[i] = rail[row][col++];
        row = dir_down ? row + 1 : row - 1;
    }
    result[len] = '\0';  // Null-terminate the result string
}

int main() {
    printf("RAIL FENCE CIPHER: \n");

    char text[] = "Hello World";
    int key = 2;
    char cipher[100];
    char decrypted[100];

    printf("The Original Text: %s\n", text);

    encrypt(text, key, cipher);
    printf("CipherText: %s\n", cipher);

    decrypt(cipher, key, decrypted);
    printf("Decrypted Text: %s\n", decrypted);

    return 0;
}

```
## OUTPUT:
![image](https://github.com/user-attachments/assets/49d20060-0aeb-4d54-83c4-d61d4eb791f3)

## RESULT:
  Thus the rail fence algorithm had been executed successfully.
