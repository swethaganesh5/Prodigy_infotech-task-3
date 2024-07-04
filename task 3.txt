import re

def check_length(password):
    """Check if the password length is at least 8 characters."""
    return len(password) >= 8

def check_uppercase(password):
    """Check if the password contains at least one uppercase letter."""
    return any(c.isupper() for c in password)

def check_lowercase(password):
    """Check if the password contains at least one lowercase letter."""
    return any(c.islower() for c in password)

def check_number(password):
    """Check if the password contains at least one number."""
    return any(c.isdigit() for c in password)

def check_special(password):
    """Check if the password contains at least one special character."""
    special_characters = re.compile(r'[!@#$%^&*(),.?":{}|<>]')
    return special_characters.search(password) is not None

def assess_strength(password):
    """Assess the strength of the password based on defined criteria."""
    criteria = [
        ('At least 8 characters', check_length(password)),
        ('At least one uppercase letter', check_uppercase(password)),
        ('At least one lowercase letter', check_lowercase(password)),
        ('At least one number', check_number(password)),
        ('At least one special character', check_special(password))
    ]
    
    # Calculate the strength score
    score = sum(1 for _, passed in criteria if passed)
    
    # Provide feedback based on score
    feedback = "Your password could be stronger. Consider adding:\n"
    for requirement, passed in criteria:
        if not passed:
            feedback += f" - {requirement}\n"
    
    return score, feedback if score < 5 else "Your password is strong!"

def main():
    password = input("Enter your password: ")
    score, feedback = assess_strength(password)
    print(f"\nPassword Strength: {score}/5")
    if score < 5:
        print(feedback)
    else:
        print("Your password is very strong!")

if __name__ == "__main__":
    main()
