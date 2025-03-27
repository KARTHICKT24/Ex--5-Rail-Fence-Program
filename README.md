# Ex--5-Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

## NAME : KARTHICK KISHORE T
## REG NO : 212223220042
## DATE 27-03-2025

# AIM:

# To write a Python program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## ALGORITHM:
```
STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.
```

## PROGRAM

```
def rail_fence_encrypt(plaintext, rails):
    if rails <= 1:
        return plaintext  # No encryption needed for 1 rail

    # Create rail matrix
    rail = [['\n' for _ in range(len(plaintext))] for _ in range(rails)]
    
    direction_down = False
    row, col = 0, 0
    
    # Fill the matrix in a zigzag pattern
    for char in plaintext:
        rail[row][col] = char
        col += 1
        
        if row == 0 or row == rails - 1:
            direction_down = not direction_down
            
        row += 1 if direction_down else -1

    # Read the characters row-wise
    encrypted_text = ''.join([''.join(row) for row in rail if row])
    return encrypted_text.replace('\n', '')  # Remove newline placeholders

def rail_fence_decrypt(ciphertext, rails):
    if rails <= 1:
        return ciphertext  # No decryption needed for 1 rail

    # Create an empty rail matrix
    rail = [['\n' for _ in range(len(ciphertext))] for _ in range(rails)]
    
    direction_down = None
    row, col = 0, 0

    # Mark positions in a zigzag pattern
    for _ in range(len(ciphertext)):
        rail[row][col] = '*'
        col += 1
        
        if row == 0:
            direction_down = True
        elif row == rails - 1:
            direction_down = False

        row += 1 if direction_down else -1

    # Fill the marked positions with ciphertext
    index = 0
    for i in range(rails):
        for j in range(len(ciphertext)):
            if rail[i][j] == '*' and index < len(ciphertext):
                rail[i][j] = ciphertext[index]
                index += 1

    # Read the decrypted message in a zigzag pattern
    row, col = 0, 0
    direction_down = None
    decrypted_text = []

    for _ in range(len(ciphertext)):
        decrypted_text.append(rail[row][col])
        col += 1

        if row == 0:
            direction_down = True
        elif row == rails - 1:
            direction_down = False

        row += 1 if direction_down else -1

    return ''.join(decrypted_text)

# Get user input
choice = input("Do you want to (E)ncrypt or (D)ecrypt? ").strip().upper()
text = input("Enter the text: ").strip()
rails = int(input("Enter the number of rails: "))

# Perform encryption or decryption
if choice == 'E':
    result = rail_fence_encrypt(text, rails)
    print(f"Encrypted Text: {result}")
elif choice == 'D':
    result = rail_fence_decrypt(text, rails)
    print(f"Decrypted Text: {result}")
else:
    print("Invalid choice! Please enter 'E' for encryption or 'D' for decryption.")

```

## OUTPUT
 # ENCRYPTION
 
 ![crypro 5 1 py](https://github.com/user-attachments/assets/98d1df43-fba4-44b1-900f-20da2b51f512)

 # DECRYPTION
 
![crypto 5 2 py](https://github.com/user-attachments/assets/e37ed8fe-f01d-45fd-86cf-01a025e80ee2)


## RESULT

THE RAIL FENCE TRANSPOSITION PROGRAM WAS IMPLEMENTED BY PYTHON PROGRAM
