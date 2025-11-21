# Exercise 1: The Palindrome Challenge
## Step 1 - Do it yourself
Before the pseudocode we must say a couple of things about the functionality of the code. The function must return a boolean value according to the result, TRUE if the string is a palindrome / FALSE if the string is not a palindrome. We must begin by taking a string argument and “break” it in an array where we have the individual letters, during this task we must also remove spaces and convert capital letters to lowercase to avoid false results. Then we start from both ends and proceed towards the middle of the slice checking every time the two letters if they are different. If we come across different letters then the function must return FALSE, since it’s not a palindrome. If the repetition process ends and we didn’t come across different letters then the string is a palindrome and the function should return TRUE.



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
            RETURN false
        left  ← left + 1
        right ← right - 1
    RETURN true

**Python implementation:**

    def is_palindrome(text):
        cleaned = ""

    # Keep only alphabet letters and convert them to lowercase
    for char in text:
        if char.isalpha():
            cleaned += char.lower()

    # Convert the string into a list of characters
    chars = list(cleaned)

    left = 0 # Set the position of the first letter
    right = len(chars) - 1 # Set the position of the last letter

    while left < right:
        if chars[left] != chars[right]:
            return False  # Different letters = It is not a palindrome

        left += 1
        right -= 1

    return True  # No mismatches = It is a palindrome

## Step 2 - Use AI to learn
- What's the time complexity?

    Your function has three phases:

    1.  Cleaning loop
        -   `cleaned += char.lower()` creates a new string each time →
            O(n²) overall.
    2.  Convert to list
        -   `list(cleaned)` → O(n).
    3.  Two‑pointer comparison
        -   Runs in O(n).

    **Overall time complexity:** O(n²)

    **Space complexity:** O(n)


- What edge cases might I miss?

    -   Unicode normalization issues (`é` vs `e` + accent)
    -   Non-Latin alphabets
    -   Characters with special casing (e.g., German **ß**)
    -   Apostrophes in words
    -   Strings with no alphabetic characters (`"123!!"` becomes empty →
        palindrome)
    -   Combining characters vs precomposed characters


- Are there better approaches?

    1. Use a list to build cleaned string (fixes O(n²))

        ``` python
        def is_palindrome(text):
            cleaned_chars = []
            for char in text:
                if char.isalpha():
                    cleaned_chars.append(char.lower())
            left = 0
            right = len(cleaned_chars) - 1
            while left < right:
                if cleaned_chars[left] != cleaned_chars[right]:
                    return False
                left += 1
                right -= 1
            return True
        ```

        **Time complexity:** O(n)

        **Space complexity:** O(n)


    2. Use slicing (Pythonic)

        ``` python
        def is_palindrome(text):
        cleaned = ''.join(c.lower() for c in text if c.isalpha())
        return cleaned == cleaned[::-1]
        ```

    3. Add Unicode normalization (more correct internationally)

        ``` python
        import unicodedata
        def is_palindrome(text):
            text = unicodedata.normalize("NFC", text)
            cleaned = ''.join(c.lower() for c in text if c.isalpha())
            return cleaned == cleaned[::-1]
        ```

## Step 3 - Reflection
- Through testing I've learned that it's easy to miss some cases like the spacing or capital letters not being equal to lowercase letters, thus providing a logical error.

- After using AI I've learned two things:
    1. Strings are already indexable in Python, so I don’t need chars = list(text) 
    2. You can save a lot of processing time.
    3. My code was based in English texts, but it is better to use Unicode so it can be applied to other languages as well.

- Yes, I'm able to create similar functions and keep in mind the cases I missed or the fact that the appliance of my code could have a broader spectrum if I want to, or need to, go to that direction.