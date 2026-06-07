# EX-NO-2: IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.

## NAME: RAJA RITHIKA
## REG NO: 2305001029



## Program:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

char keyT[5][5];

void generateKey(char key[]) {
    int used[26]={0}, k=0;
    used['j'-'a']=1;

    for(int i=0; key[i]; i++) {
        char ch=tolower(key[i]);
        if(!used[ch-'a']) {
            keyT[k/5][k%5]=ch;
            used[ch-'a']=1;
            k++;
        }
    }

    for(int i=0;i<26;i++)
        if(!used[i])
            keyT[k/5][k%5]=i+'a', k++;
}

void find(char ch,int *r,int *c) {
    if(ch=='j') ch='i';
    for(int i=0;i<5;i++)
        for(int j=0;j<5;j++)
            if(keyT[i][j]==ch)
                *r=i,*c=j;
}

void process(char str[], int mode) {
    int r1,c1,r2,c2;

    for(int i=0; str[i]; i+=2) {
        find(str[i],&r1,&c1);
        find(str[i+1],&r2,&c2);

        if(r1==r2) {
            str[i]=keyT[r1][(c1+mode+5)%5];
            str[i+1]=keyT[r2][(c2+mode+5)%5];
        }
        else if(c1==c2) {
            str[i]=keyT[(r1+mode+5)%5][c1];
            str[i+1]=keyT[(r2+mode+5)%5][c2];
        }
        else {
            str[i]=keyT[r1][c2];
            str[i+1]=keyT[r2][c1];
        }
    }
}

int main() {
    char text[100], key[100];

    printf("Enter key: ");
    scanf("%s", key);

    printf("Enter text: ");
    scanf("%s", text);

    generateKey(key);

    process(text, 1);
    printf("Encrypted: %s\n", text);

    process(text, -1);
    printf("Decrypted: %s", text);
}
```





## Output:

<img width="548" height="230" alt="image" src="https://github.com/user-attachments/assets/8dcc62ab-507b-4019-89ce-ef058a65dbc2" />




## Result:

Hence the program has been executed successfully
