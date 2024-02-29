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
import numpy as np

def generate_key_matrix(key):
    key = key.upper().replace(" ", "")
    n = int(len(key) ** 0.5)
    if n * n != len(key):
        raise ValueError("Key length must be a perfect square")
    key_matrix = np.array([ord(char) - ord('A') for char in key]).reshape(n, n)
    return key_matrix

def generate_inverse_key_matrix(key_matrix):
    determinant = np.linalg.det(key_matrix)
    inverse_matrix = np.linalg.inv(key_matrix)
    adjugate_matrix = np.round(inverse_matrix * determinant).astype(int)
    det_inv = pow(int(determinant), -1, 26)
    inverse_key_matrix = (adjugate_matrix * det_inv) % 26
    return inverse_key_matrix

## ENCRYPTION

def hill_encrypt(plain_text, key_matrix):
    plain_text = plain_text.upper().replace(" ", "").replace("J", "I")
    n = key_matrix.shape[0]
    while len(plain_text) % n != 0:
        plain_text += 'X'
    plain_text = [ord(char) - ord('A') for char in plain_text]
    plain_matrix = np.array(plain_text).reshape(-1, n)
    encrypted_matrix = np.dot(plain_matrix, key_matrix) % 26
    encrypted_text = ""
    for row in encrypted_matrix:
        for char in row:
            encrypted_text += chr(char + ord('A'))
    return encrypted_text

## DECRYPTION

def hill_decrypt(encrypted_text, key_matrix):
    n = key_matrix.shape[0]
    inverse_key_matrix = generate_inverse_key_matrix(key_matrix)
    encrypted_text = encrypted_text.upper().replace(" ", "").replace("J", "I")
    encrypted_text = [ord(char) - ord('A') for char in encrypted_text]
    encrypted_matrix = np.array(encrypted_text).reshape(-1, n)
    decrypted_matrix = np.dot(encrypted_matrix, inverse_key_matrix) % 26
    decrypted_text = ""
    for row in decrypted_matrix:
        for char in row:
            decrypted_text += chr(char + ord('A'))
    return decrypted_text

key = "HILL"
plaintext = "SANJAY"
key_matrix = generate_key_matrix(key)

encrypted_text = hill_encrypt(plaintext, key_matrix)
print("Plaintext:", plaintext)
print("Encrypted text:", encrypted_text)


decrypted_text = hill_decrypt(encrypted_text, key_matrix)
print("Decrypted text:", decrypted_text)

```
## OUTPUT:
![image](https://github.com/sanjay3061/Cryptography---19CS412-classical-techqniques/assets/121215929/b3b133bc-ca5c-42fe-adcd-058b165e6f79)

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

## ENCRYPTION

def vigenere_encrypt(plain_text, key):
    key = key.upper()
    encrypted_text = ""
    key_index = 0
    for char in plain_text:
        if char.isalpha():
            shift = ord(key[key_index % len(key)]) - ord('A')
            if char.islower():
                encrypted_char = chr((ord(char) - ord('a') + shift) % 26 + ord('a'))
            else:
                encrypted_char = chr((ord(char) - ord('A') + shift) % 26 + ord('A'))
            encrypted_text += encrypted_char
            key_index += 1
        else:
            encrypted_text += char
    return encrypted_text

## DECRYPTION

def vigenere_decrypt(encrypted_text, key):
    key = key.upper()
    decrypted_text = ""
    key_index = 0
    for char in encrypted_text:
        if char.isalpha():
            shift = ord(key[key_index % len(key)]) - ord('A')
            if char.islower():
                decrypted_char = chr((ord(char) - ord('a') - shift + 26) % 26 + ord('a'))
            else:
                decrypted_char = chr((ord(char) - ord('A') - shift + 26) % 26 + ord('A'))
            decrypted_text += decrypted_char
            key_index += 1
        else:
            decrypted_text += char
    return decrypted_text

plain_text = "SANJAY"
key = "cipher"
encrypted_text = vigenere_encrypt(plain_text, key)
print("Original Text:", plain_text)
print("Encrypted Text:", encrypted_text)

decrypted_text = vigenere_decrypt(encrypted_text, key)
print("Decrypted Text:", decrypted_text)
```
## OUTPUT:
![image](https://github.com/sanjay3061/Cryptography---19CS412-classical-techqniques/assets/121215929/7ca3a140-289e-44cc-b581-a5bd269ae350)

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

## ENCRYPTION

def rail_fence_encrypt(plain_text, key):
    encrypted_text = ""
    rail = [''] * key
    direction = False
    row = 0

    for char in plain_text:
        rail[row] += char
        if row == 0 or row == key - 1:
            direction = not direction
        row += 1 if direction else -1

    for i in range(key):
        encrypted_text += rail[i]

    return encrypted_text

## DECRYPTION

def rail_fence_decrypt(encrypted_text, key):
    decrypted_text = ""
    rail = [''] * key
    direction = False
    row = 0
    index = 0

    for char in encrypted_text:
        rail[row] += '*'
        if row == 0 or row == key - 1:
            direction = not direction
        row += 1 if direction else -1

    for i in range(key):
        for j in range(len(rail[i])):
            if rail[i][j] == '*' and index < len(encrypted_text):
                rail[i] = rail[i][:j] + encrypted_text[index] + rail[i][j + 1:]
                index += 1

    row = 0
    direction = False
    for i in range(len(encrypted_text)):
        decrypted_text += rail[row][0]
        rail[row] = rail[row][1:]
        if row == 0 or row == key - 1:
            direction = not direction
        row += 1 if direction else -1

    return decrypted_text

plain_text = "SANJAY"
key = 3
encrypted_text = rail_fence_encrypt(plain_text, key)
print("Original Text:", plain_text)
print("Encrypted Text:", encrypted_text)

decrypted_text = rail_fence_decrypt(encrypted_text, key)
print("Decrypted Text:", decrypted_text)
```
## OUTPUT:
![image](https://github.com/sanjay3061/Cryptography---19CS412-classical-techqniques/assets/121215929/045f7b42-7f54-4510-ba68-73fdfb3a0504)

## RESULT:
The program is executed successfully
