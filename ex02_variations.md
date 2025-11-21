# Exercise 2: Strengthening Through Variations
1. Modifications for **ignoring spaces and punctuation** and **being case-insensitive** are already in the code so there is no reason to modify it further.

Modifying the pseudocode and the code so we can return the position where the string stops being a palindrome (if not one).

**Pseudocode:**

    function isItPalindrome(str):
    cleaned ← empty string
    FOR each char in str:
        IF char is an alphabet letter:
            cleaned ← cleaned + lowercase(char)
    left  ← 0
    right ← length(cleaned) - 1
    WHILE left < right:
        IF cleaned[left] <> cleaned[right]:
            RETURN false, left, right  
        left  ← left + 1
        right ← right - 1
    RETURN true, -1, -1

**Python implementation:**

    def is_palindrome(text):
        cleaned = ""

    for char in text:
        if char.isalpha():
            cleaned += char.lower()

    chars = list(cleaned)

    left = 0 
    right = len(chars) - 1 

    while left < right:
        if chars[left] != chars[right]:
            return False, left, right # Returns the boolean and the index of mismatch

        left += 1
        right -= 1

    return True, -1, -1 # We need the -1 otherwise there would be a problem with the return values