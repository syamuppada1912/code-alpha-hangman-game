# code-alpha-hangman-game
import random

# List of words to choose from
word_list = [
    "hangman",
    "python",
    "programming",
    "computer",
    "science",
    "algorithm",
    "openai"
]

def select_random_word():
    return random.choice(word_list)

def display_word(word, guessed_letters):
    """
    Display the current state of the word with underscores for unguessed letters
    """
    display = ""
    for letter in word:
        if letter in guessed_letters:
            display += letter + " "
        else:
            display += "_ "
    return display.strip()

def hangman():
    print("Welcome to Hangman!")
    
    # Select a random word from the list
    secret_word = select_random_word()
    guessed_letters = []
    incorrect_guesses = 0
    max_incorrect_guesses = 6  # Adjust this number as desired
    
    while True:
        print("\nCurrent word: ", display_word(secret_word, guessed_letters))
        print("Guessed letters: ", guessed_letters)
        
        # Get a guess from the player
        guess = input("Guess a letter: ").lower()
        
        # Check if the guess is a single letter
        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single letter.")
            continue
        
        # Check if the letter has already been guessed
        if guess in guessed_letters:
            print("You've already guessed that letter.")
            continue
        
        # Add the guessed letter to the list
        guessed_letters.append(guess)
        
        # Check if the guessed letter is in the secret word
        if guess in secret_word:
            print("Correct!")
        else:
            print("Incorrect!")
            incorrect_guesses += 1
        
        # Check if the player has won
        if all(letter in guessed_letters for letter in secret_word):
            print("\nCongratulations! You guessed the word:", secret_word)
            break
        
        # Check if the player has lost
        if incorrect_guesses >= max_incorrect_guesses:
            print("\nSorry, you've run out of guesses!")
            print("The word was:", secret_word)
            break

# Run the game
hangman()
