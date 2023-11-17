# Hangman

import random

easy_words = ["python", "variable", "loop", "list"]
medium_words = ["function", "conditional", "module", "class"]
hard_words = ["dictionary", "object", "recursion", "inheritance"]

def choose_word(difficulty):
    if difficulty == "easy":
        return random.choice(easy_words)
    elif difficulty == "medium":
        return random.choice(medium_words)
    elif difficulty == "hard":
        return random.choice(hard_words)
    else:
        raise ValueError("Invalid difficulty level")

def initialize_game():
    global word_to_guess, guessed_letters, max_guesses, incorrect_guesses, display_word

    difficulty = input("Choose a difficulty level (easy, medium, hard): ").lower()
    word_to_guess = choose_word(difficulty)

    guessed_letters = []
    max_guesses = 10
    incorrect_guesses = 0
    display_word = ["_"] * len(word_to_guess)

def display_current_state():
    print(" ".join(display_word))
    print(f"Guessed letters: {' '.join(guessed_letters)}")
    print(f"Guesses left: {max_guesses - incorrect_guesses}")

while True:
    initialize_game()

    while True:
        display_current_state()

        if "_" not in display_word:
            print("Congratulations! You've guessed the word correctly.")
            break

        if incorrect_guesses >= max_guesses:
            print("You've run out of guesses. The word was:", word_to_guess)
            break

        guess = input("Guess a letter: ").lower()

        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single letter.")
            continue

        if guess in guessed_letters:
            print("You've already guessed that letter.")
            continue

        guessed_letters.append(guess)

        if guess in word_to_guess:
            for i in range(len(word_to_guess)):
                if word_to_guess[i] == guess:
                    display_word[i] = guess
        else:
            incorrect_guesses += 1
