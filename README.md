# hangman-game
import random

# Predefined list of 5 words
word_list = ["apple", "train", "house", "plant", "chair"]

# Select a random word from the list
secret_word = random.choice(word_list)

# Game state
guessed_letters = []
wrong_guesses = 0
max_wrong_guesses = 6

# Create a display version of the word (e.g., "_ _ _ _ _")
display_word = ["_"] * len(secret_word)

print("🎮 Welcome to Hangman!")
print("Guess the word, one letter at a time.")
print("You have 6 chances to make mistakes.\n")

# Main game loop
while wrong_guesses < max_wrong_guesses and "_" in display_word:
    print("Word:", " ".join(display_word))
    guess = input("Guess a letter: ").lower()

    if not guess.isalpha() or len(guess) != 1:
        print("Please enter a single alphabet letter.\n")
        continue

    if guess in guessed_letters:
        print("You already guessed that letter.\n")
        continue

    guessed_letters.append(guess)

    if guess in secret_word:
        # Reveal the letter in the display
        for i in range(len(secret_word)):
            if secret_word[i] == guess:
                display_word[i] = guess
        print("✅ Correct guess!\n")
    else:
        wrong_guesses += 1
        print(f"❌ Wrong guess! {max_wrong_guesses - wrong_guesses} tries left.\n")

# Game result
if "_" not in display_word:
    print("🎉 Congratulations! You guessed the word:", secret_word)
else:
    print("💀 Game Over! The word was:", secret_word)
