This project is part of Freecodecamp's [Scientific Computing with Python](https://www.freecodecamp.org/learn/scientific-computing-with-python/) curriculum

```py
import re
import secrets # Module for generating cryptographically secure random numbers.
import string


def generate_password(length=8, nums=1, special_chars=1, uppercase=1, lowercase=1):

    # Define the possible characters for the password
    letters = string.ascii_letters
    digits = string.digits
    symbols = string.punctuation

    # Combine all characters
    all_characters = letters + digits + symbols

    while True:
        password = ''
        # Generate password
        for _ in range(length):
            password += secrets.choice(all_characters) # To make a random choice from a given sequence (e.g., a string or a list). It's more secure than using random.choice because it is designed to be resistant to various attacks on pseudo-random number generators.
        
        constraints = [
            (nums, r'\d'),
            (special_chars, fr'[{symbols}]'),
            (uppercase, r'[A-Z]'),
            (lowercase, r'[a-z]')
        ]

        # Check constraints        
        if all(
            constraint <= len(re.findall(pattern, password)) 
            for constraint, pattern in constraints
        ):
            break

# The generator expression iterates through each constraint and pattern in the constraints list. For each constraint and pattern, it checks whether the count of characters in the generated password that match the pattern is greater than or equal to the specified constraint. 
        
# all() checks whether the condition is True or not. It returns True if all elements of the iterable are true.
               
    return password
    
if __name__ == '__main__':
    new_password = generate_password() # You can remove the default value and pass values here.
    print('Generated password:', new_password)
```