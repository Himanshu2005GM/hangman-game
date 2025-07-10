import random

word_list = ['apple', 'house', 'train', 'beach', 'robot']
chosen_word = random.choice(word_list)

display = ['_' for _ in chosen_word]

max_attempts = 6
wrong_guesses = 0
guessed_letters = []

print("Welcome to Hangman!")
print("Guess the word, one letter at a time.")

while wrong_guesses < max_attempts and '_' in display:
    print("\nWord: ", ' '.join(display))
    print(f"Wrong guesses left: {max_attempts - wrong_guesses}")
    guess = input("Enter a letter: ").lower()

    if not guess.isalpha() or len(guess) != 1:
        print("Please enter a single letter.")
        continue

    if guess in guessed_letters:
        print("You've already guessed that letter.")
        continue

    guessed_letters.append(guess)

    if guess in chosen_word:
        print(f"Good guess! '{guess}' is in the word.")
        for i in range(len(chosen_word)):
            if chosen_word[i] == guess:
                display[i] = guess
    else:
        print(f"Sorry, '{guess}' is not in the word.")
        wrong_guesses += 1

if '_' not in display:
    print("\nCongratulations! You guessed the word:", chosen_word)
else:
    print("\nGame Over! The word was:", chosen_word)
