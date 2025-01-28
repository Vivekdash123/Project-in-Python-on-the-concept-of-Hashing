1. Importing the hashlib module

import hashlib
The hashlib module is a built-in Python library that provides various cryptographic hash functions, including SHA-256, which is used in this project to hash the passwords.
2. Defining the hash_password function

def hash_password(password):
    sha256 = hashlib.sha256()
    sha256.update(password.encode('utf-8'))
    return sha256.hexdigest()
    
This function hashes a given password using the SHA-256 algorithm.
hashlib.sha256() creates a new SHA-256 hash object. SHA-256 is a cryptographic hash function that takes an input (like a password) and produces a fixed-length (256-bit) hash value.
password.encode('utf-8') converts the password string (which is a sequence of characters) into a byte sequence, because the hashing function operates on bytes, not on strings directly.
sha256.update() is called to "feed" the byte-encoded password into the hash object.
sha256.hexdigest() generates and returns the final hash in the form of a hexadecimal string (which is easier to store or display).
3. Creating a simulated user database

user_database = {}

Here, we create a simple dictionary called user_database to simulate a user database where we will store usernames as keys and their corresponding hashed passwords as values.
This allows us to check whether a user exists and if their password matches a stored one.
4. Defining the add_user function

def add_user(username, password):
    hashed_password = hash_password(password)
    user_database[username] = hashed_password
    print(f"User '{username}' added with hashed password.")
    
This function adds a user to the database with their username and hashed password.
hash_password(password) is called to hash the password passed as an argument to the function.
The username is used as the key, and the hashed password is the value stored in the user_database dictionary.
A message is printed to indicate that the user has been added successfully with their hashed password.
5. Defining the verify_user function

def verify_user(username, password):
    if username in user_database:
        hashed_password = hash_password(password)
        if user_database[username] == hashed_password:
            print(f"Password for user '{username}' is correct.")
        else:
            print(f"Incorrect password for user '{username}'.")
    else:
        print(f"User '{username}' not found.")
        
This function verifies if a given password matches the hashed password stored for a specific username.
First, the function checks if the username exists in the user_database. If it does:
It hashes the password passed to the function.
The function then compares the hashed version of the entered password to the stored hashed password in the dictionary.
If the passwords match, it prints a message confirming the correct password.
If the passwords do not match, it prints a message saying the password is incorrect.
If the username does not exist in the user_database, the function prints a message saying the user is not found.
6. Adding and verifying users

add_user('Alice', 'my_secure_password')
add_user('Bob', 'another_password')
verify_user('Alice', 'my_secure_password')  # Correct password
verify_user('Alice', 'wrong_password')      # Incorrect password
verify_user('Charlie', 'some_password')     # User not found

Adding Users:
The add_user() function is called twice:
The first call adds "Alice" with the password "my_secure_password".
The second call adds "Bob" with the password "another_password".
Verifying Users:
The verify_user() function is then called three times:
The first call checks if "Alice" has entered the correct password ("my_secure_password").
The second call checks if "Alice" entered an incorrect password ("wrong_password").
The third call checks if a user named "Charlie" exists, but "Charlie" hasn't been added yet, so it will print "User 'Charlie' not found."

7. Example Output
If you run the code, the output would look something like this:

User 'Alice' added with hashed password.
User 'Bob' added with hashed password.
Password for user 'Alice' is correct.
Incorrect password for user 'Alice'.
User 'Charlie' not found.

First two lines: "Alice" and "Bob" are added to the user_database with their respective hashed passwords.
Next line: It verifies that Alice entered the correct password.
Next line: It verifies that Alice did not enter the correct password.
Last line: It checks for a non-existent user "Charlie" and prints that the user wasn't found.
