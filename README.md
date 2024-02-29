# Cryptography---19CS412-classical-techqniques


# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To develop a simple C program to implement Caeser Cipher.

## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
## Encryption:

def caesar_cipher(text, shift):
    encrypted_text = ""
    for char in text:
        if char.isalpha():  # Check if the character is alphabet
            shifted = ord(char) + shift
            if char.islower():
                if shifted > ord('z'):
                    shifted -= 26
                elif shifted < ord('a'):
                    shifted += 26
            elif char.isupper():
                if shifted > ord('Z'):
                    shifted -= 26
                elif shifted < ord('A'):
                    shifted += 26
            encrypted_text += chr(shifted)
        else:
            encrypted_text += char
    return encrypted_text
text = "SANJAY"
shift = 3


encrypted_text = caesar_cipher(text, shift)
print("Original Text:", text)
print("Encrypted Text:", encrypted_text)

## Decryption:

def caesar_decrypt(encrypted_text, shift):
    decrypted_text = ""
    for char in encrypted_text:
        if char.isalpha():  # Check if the character is alphabet
            shifted = ord(char) - shift
            if char.islower():
                if shifted > ord('z'):
                    shifted -= 26
                elif shifted < ord('a'):
                    shifted += 26
            elif char.isupper():
                if shifted > ord('Z'):
                    shifted -= 26
                elif shifted < ord('A'):
                    shifted += 26
            decrypted_text += chr(shifted)
        else:
            decrypted_text += char
    return decrypted_text


text = "SANJAY"
shift = 3

decrypted_text = caesar_decrypt(encrypted_text, shift)
print("Decrypted Text:", decrypted_text)
```
## OUTPUT:
![image](https://github.com/sanjay3061/Cryptography---19CS412-classical-techqniques/assets/121215929/86cceaf4-129a-4751-aa56-dc9f6249d828)

## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To develop a simple C program to implement PlayFair Cipher.

## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```

def prepare_text(text):
    text = text.replace(" ", "").upper()
    if len(text) % 2 != 0:
        text += 'X'
    return text

def generate_playfair_matrix(key):
    key = key.replace(" ", "").upper()
    # Create a set of unique characters in the key
    key_set = []
    for char in key:
        if char not in key_set and char != 'J':  # Replace 'J' with 'I'
            key_set.append(char)
   
    alphabet = "ABCDEFGHIKLMNOPQRSTUVWXYZ"
    matrix = [key_set]
    for char in alphabet:
        if char not in key_set:
            matrix[-1].append(char)
            if len(matrix[-1]) == 5:
                matrix.append([])
    return matrix

def get_char_position(matrix, char):
    for i, row in enumerate(matrix):
        if char in row:
            return i, row.index(char)
    raise ValueError(f"Character '{char}' not found in the matrix.")

## ENCRYPTION

def playfair_encrypt(plaintext, key):
    plaintext = prepare_text(plaintext)
    matrix = generate_playfair_matrix(key)
    ciphertext = ""
    for i in range(0, len(plaintext), 2):
        char1, char2 = plaintext[i], plaintext[i+1]
        row1, col1 = get_char_position(matrix, char1)
        row2, col2 = get_char_position(matrix, char2)
        if row1 == row2:  # Characters are in the same row
            ciphertext += matrix[row1][(col1 + 1) % 5]
            ciphertext += matrix[row2][(col2 + 1) % 5]
        elif col1 == col2:  # Characters are in the same column
            ciphertext += matrix[(row1 + 1) % 5][col1]
            ciphertext += matrix[(row2 + 1) % 5][col2]
        else:  # Characters form a rectangle
            ciphertext += matrix[row1][col2]
            ciphertext += matrix[row2][col1]
    return ciphertext

## DECRYPTION

def playfair_decrypt(ciphertext, key):
    ciphertext = prepare_text(ciphertext)
    matrix = generate_playfair_matrix(key)
    plaintext = ""
    for i in range(0, len(ciphertext), 2):
        char1, char2 = ciphertext[i], ciphertext[i+1]
        row1, col1 = get_char_position(matrix, char1)
        row2, col2 = get_char_position(matrix, char2)
        if row1 == row2:  # Characters are in the same row
            plaintext += matrix[row1][(col1 - 1) % 5]
            plaintext += matrix[row2][(col2 - 1) % 5]
        elif col1 == col2:  # Characters are in the same column
            plaintext += matrix[(row1 - 1) % 5][col1]
            plaintext += matrix[(row2 - 1) % 5][col2]
        else:  # Characters form a rectangle
            plaintext += matrix[row1][col2]
            plaintext += matrix[row2][col1]
    return plaintext

plaintext = "SAVEETHA"
key = "Sanjay"

encrypted_text = playfair_encrypt(plaintext, key)
print("Key:",key)
print("Original Text:", plaintext)
print("Encrypted Text:", encrypted_text)


decrypted_text = playfair_decrypt(encrypted_text, key)
print("Decrypted Text:", decrypted_text)



```
## OUTPUT:
![image](https://github.com/sanjay3061/Cryptography---19CS412-classical-techqniques/assets/121215929/07e37c83-abd3-422a-826e-e00cc7656eea)

## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include<stdio.h>
#include<conio.h>
#include<string.h>
int main(){
unsigned int a[3][3]={{6,24,1},{13,16,10},{20,17,15}};
unsigned int b[3][3]={{8,5,10},{21,8,21},{21,12,8}};
int i,j, t=0;
unsigned int c[20],d[20];
char msg[20];
printf("Enter plain text: ");
scanf("%s",msg);
for(i=0;i<strlen(msg);i++)
{
c[i]=msg[i]-65;
unsigned int a[3][3]={{6,24,1},{13,16,10},{20,17,15}};
unsigned int b[3][3]={{8,5,10},{21,8,21},{21,12,8}};
printf("%d ",c[i]);
}
for(i=0;i<3;i++)
{ t=0;
for(j=0;j<3;j++)
{
t=t+(a[i][j]*c[j]);
}
d[i]=t%26;
}
printf("\nEncrypted Cipher Text :");
for(i=0;i<3;i++)
printf(" %c",d[i]+65);
for(i=0;i<3;i++)
{
t=0;
for(j=0;j<3;j++)
{
t=t+(b[i][j]*d[j]);
}
c[i]=t%26;
}
printf("\nDecrypted Cipher Text :");
for(i=0;i<3;i++)
printf(" %c",c[i]+65);
getch();
return 0;
}
```
## OUTPUT:
![Screenshot 2024-02-29 181124](https://github.com/sanjay3061/Cryptography---19CS412-classical-techqniques/assets/121215929/4b655394-b915-41cb-b26e-d34eda805007)

## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>
#include<conio.h>
#include <ctype.h>
#include <string.h>
void encipher();
void decipher();
int main()
{
int choice;
while(1)
{
printf("\n\nEnter Your Choice : ");
scanf("%d",&choice);
if(choice == 3)
exit(0);
else if(choice == 1)
encipher();
else if(choice == 2)
decipher();
else
printf("Please Enter Valid Option.");
}
}
void encipher()
{
unsigned int i,j;
char input[50],key[10];
printf("\n\nEnter Plain Text: ");
scanf("%s",input);
printf("\nEnter Key Value: ");
scanf("%s",key);
printf("\nResultant Cipher Text: ");
for(i=0,j=0;i<strlen(input);i++,j++)
{
if(j>=strlen(key))
{ j=0;
}
printf("%c",65+(((toupper(input[i])-65)+(toupper(key[j])-
65))%26));
}}
void decipher()
{
unsigned int i,j;
char input[50],key[10];
int value;
printf("\n\nEnter Cipher Text: ");
scanf("%s",input);
printf("\n\nEnter the key value: ");
scanf("%s",key);
for(i=0,j=0;i<strlen(input);i++,j++)
{
if(j>=strlen(key))
{ j=0; }
value = (toupper(input[i])-64)-(toupper(key[j])-64);
if( value < 0)
{ value = value * -1;
}
printf("%c",65 + (value % 26));
}
return 0;
}
```
## OUTPUT:
![image](https://github.com/sanjay3061/Cryptography---19CS412-classical-techqniques/assets/121215929/28df34bd-9b1d-4781-a9d0-89b6be2ffcd8)

## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include<stdio.h>
#include<conio.h>
#include<string.h>
int main()
{
int i,j,k,l;
char a[20],c[20],d[20];
printf("\n\t\t RAIL FENCE TECHNIQUE");
printf("\n\nEnter the input string : ");
gets(a);
l=strlen(a);

for(i=0,j=0;i<l;i++)
{
if(i%2==0)
c[j++]=a[i];
}
for(i=0;i<l;i++)
{
if(i%2==1)
c[j++]=a[i];
}
c[j]='\0';
printf("\nCipher text after applying rail fence :");
printf("\n%s",c);

if(l%2==0)
k=l/2;
else
k=(l/2)+1;
for(i=0,j=0;i<k;i++)
{
d[j]=c[i];
j=j+2;
}
for(i=k,j=1;i<l;i++)
{
d[j]=c[i];
j=j+2;
}
d[l]='\0';
printf("\nText after decryption : ");
printf("%s",d);
return 0;
}
```
## OUTPUT:
![image](https://github.com/sanjay3061/Cryptography---19CS412-classical-techqniques/assets/121215929/f7288e4f-f7bd-489f-ba7d-566c094f23ee)

## RESULT:
The program is executed successfully
