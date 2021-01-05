# Hangman-Game
Using Python to create a simple word game, Hangman  Below is a very detailed explanation of the code I used to create this game, in order for others reading this to understand as well as a point of reference to revert back to as my Python skills improve, we import a predetermined list of upper-case characters in the dictionary. I randomly select a word from a list of words then continuously ask for user input until you win. Then, I incorporate lives so you can't get unlimited guesses

import random 

- To be able to import randomly from my word list 

from words import words

- I have created a words file with a long list of common english words obtained from stack overflow. Within that file I've created a variable called words and assigned the words, so from words (word file), import words (the variable words)

import string

- We import a predetermined list of upper case characters in the dictionary

def get_valid_word(words):

- Defining a function and passing it a list of words, in order to get a valid word, not one with a space

word = random.choice(words)  # randomly chooses something from the list
    
- We assign the word found to random.choice. This takes in a list and randomly choosing something from this list 

while '-' in word or ' ' in word:
word = random.choice(words)
        
- While loop is saying while dash or space is in the word, keep choosing another word, keeps iterating until it finds a words without this

return word.upper()
- finally once it finds a word that fits it will return the word

def hangman():

- We need to keep track of which letters we have guessed and which letters in the word we have correctly guessed as well as keep track of what a valid letter is and what isn't, we have done this below
    
word = get_valid_word(words)
word_letters = set(word)  # letters in the word

- This variable (word_letters) saves all the letters in a word as a set and this will keep track of what has been guessed in the word

alphabet = set(string.ascii_uppercase)
    
- We have an alphabet and link it to the string import we did at the beginning 

used_letters = set()  # what the user has guessed
    
- we have an empty set to keep track of what the user has guessed

    lives = 6

-	We are giving the user lives 

# getting user input
    
while len(word_letters) > 0 and lives > 0:

-	While the length of word letters is greater than 0, keep iterating through the input until they guess all the letters and lives greater than 0, then we want the user to guess. So they exit the while loop when they died or guessed all the letters

# letters used
# ' '.join(['a', 'b', 'cd']) --> 'a b cd'
print('You have', lives, 'lives left and you have used these letters: ', ' '.join(used_letters))

-	We need to tell the user how many live they have, what letter they have used; the print statement will tell them. The .join, turns the iterated into a string separated by, whatever the string is before the .join 

# what current word is (ie W - R D)
       
word_list = [letter if letter in used_letters else '-' for letter in word]

-	We also need to tell the user what the current word is, with dashes where the characters that they haven’t guessed are. So, we create a list which shows the correct letter guessed and dashes for remaining

print('Current word: ', ' '.join(word_list))

-	Then take that list and join it with a space and create a string using that list

user_letter = input('Guess a letter: ').upper()

- we can ask for user input in Python directly and run this in terminal as input. We save this as a letter and use upper case in order to test equality between strings
        
if user_letter in alphabet - used_letters:
        
- If this is a valid character in the alphabet that I haven't used yet,

used_letters.add(user_letter)

- then I am going to add this to my used letter set

if user_letter in word_letters:

- If the letter that I just guessed is in the word 
                
word_letters.remove(user_letter)
                
- Then I am going to remove that letter from word letters, so every single time that I guess correctly, so every single time I guess correctly, this word letter decreases 
print('')

else:
lives = lives - 1  # takes away a life if wrong
-	If the user does not have the letter in word_letters, take away 1 life

print('\nYour letter,', user_letter, 'is not in the word.')
-	Tell the user that the letter is not in the word

elif user_letter in used_letters:

- Then, if this letter that the user just entered is in used letters, that means they have already used it and it is invalid so print the below 

print('\nYou have already used that letter. Guess another letter.')

else:
print('\nThat is not a valid letter.')
- Otherwise it means they have entered something that is not in the alphabet, so it's a wrong character so print the above error message

# gets here when len(word_letters) == 0 OR when lives == 0
if lives == 0:

-	So if the users lives = 0, they have died and we print the below
print('You died, sorry. The word was', word)

else:
print('YAY! You guessed the word', word, '!!')

-	Otherwise, they have guessed right, so we print the above

if __name__ == '__main__':

- This code prevents (certain) code from being run when the module is imported.
    hangman()
