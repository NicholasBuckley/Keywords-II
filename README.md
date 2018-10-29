// Keywords II
//Nicholas Buckley 10.28.2018

#include "pch.h"
#include "pch.h"
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <ctime>
#include <cctype>

using namespace std;

//Creating the main function
int main()
{

	char again; // To rerun simulation
	string user; // For user's name
	int simulation, correct, finish, fail;
	// Create an int var to count the number of simulations being run starting at 1
	simulation = 1; // To track simulation

	// Display Tittle of program to user
	cout << "\t\t\Welcome to the Code Breaker Training Simulation!\n\n";
	// Ask the recruit to login using their name
	cout << "Please enter your code name for this assignment: \n";
	// Hold the recruit's name in a var, and address them by it throughout the simulation.
	cin >> user;
	cout << "\nWelcome " << user << "\n\n";
	// Display an overview of what Keywords II is to the recruit
	// Display an directions to the recruit on how to use Keywords
	cout << "In this simulation you are going to be assigned a secret code word.\n";
	cout << "You are going to have 8 chances to guess the letters in the code word.\n";
	cout << "You will be told if the letter you enter is in the code word or not.\n";
	cout << "Displayed will be the letters that you have already used and where they are located in the word.\n";
	cout << "Once you believe you know the code word enter your guess.\n";
	cout << "If you do not get the code word in your 8 guesses you fail.\n";
	cout << "You must complete 3 code words to complete this simulation.\n";



	const int MAX_WRONG = 8;  // maximum number of incorrect guesses allowed

	// Create a collection of 10 words you had wrote down manually
	vector<string> words;  // collection of possible words to guess
	words.push_back("ROCKET");
	words.push_back("BULLET");
	words.push_back("PASSWORD");
	words.push_back("SILENCER");
	words.push_back("UNDERCOVER");
	words.push_back("TARGET");
	words.push_back("KNIFE");
	words.push_back("BOMB");
	words.push_back("DEFUSE");
	words.push_back("HITMAN");

	do //continue playing
	{


		correct = 0;
		finish = 3;
		fail = 1;
		// Display the simulation # is staring to the recruit.
		cout << "\n====================================================================================================================\n"; // Spacing
		cout << "This is simulation " << simulation << ".\n\n";//     Move program execution back up to // Display the simulation # is staring to the recruit.
		cout << "Good Luck " << user << "!\n";
		cout << "====================================================================================================================\n"; // Spacing

		do // Continue playing until solving 3 words
		{
			srand(static_cast<unsigned int>(time(0)));
			random_shuffle(words.begin(), words.end());
			const string THE_WORD = words[0]; // The word assigned
			int wrong = 0;     // Number of incorrect guesses                          
			string soFar(THE_WORD.size(), '-');   // Word created so sofar
			string used = "";     // Letters already guessed



	 // Pick new 3 random words from your collection as the secret code word the recruit has to guess. 
			// While recruit hasn’t made too many incorrect guesses and hasn’t guessed the secret word
			while ((wrong < MAX_WRONG) && (soFar != THE_WORD))
			{
				//     Tell recruit how many incorrect guesses he or she has left
				cout << "\n\nYou have " << (MAX_WRONG - wrong);
				//          Increment the number of incorrect guesses the recruit has made
				cout << " incorrect guesses left.\n";
				//     Show recruit the letters he or she has guessed
				cout << "\nYou've used the following letters:\n" << used << endl;
				//     Show player how much of the secret word he or she has guessed
				cout << "\nSo far, the word is:\n" << soFar << endl;

				//     Get recruit's next guess
				char guess;
				cout << "\n\nEnter your guess: ";
				cin >> guess;
				guess = toupper(guess); //make uppercase since secret word in uppercase
				while (used.find(guess) != string::npos)
				{
					//     While recruit has entered a letter that he or she has already guessed
					cout << "\nYou've already guessed " << guess << endl;
					//          Get recruit ’s guess
					cout << "Enter your guess: ";
					cin >> guess;
					//     Add the new guess to the group of used letters
					guess = toupper(guess);
				}

				used += guess;

				//     If the guess is in the secret word
				if (THE_WORD.find(guess) != string::npos)
				{
					//          Tell the recruit the guess is correct
					cout << "That's right! " << guess << " is in the word.\n";

					//          Update the word guessed so far with the new letter
					for (unsigned int i = 0; i < THE_WORD.length(); ++i)
					{
						if (THE_WORD[i] == guess)
						{
							soFar[i] = guess;
						}
					}
				}
				//     Otherwise
				else
				{
					//          Tell the recruit the guess is incorrect
					cout << "Sorry, " << guess << " isn't in the word.\n";
					++wrong;
				}
			}


			// If the recruit has made too many incorrect guesses
			if (wrong == MAX_WRONG)
			{
				//     Tell the recruit that he or she has failed the Keywords II course.
				cout << "\nYou have failed the simulation!";
				correct = 3; // End game if incorrect limit reached
			}
			// Otherwise
			else
			{
				//     Congratulate the recruit on guessing the secret words
				cout << "====================================================================================================================\n"; // Spacing
				cout << "\nYou have correctly guess the code!\n";
				++correct;
				cout << "Successfully completed codes: " << correct << ".\n";

			}
			cout << "\nThe word was " << THE_WORD << endl;;
			cout << "====================================================================================================================\n"; // Spacing

		} while (correct != finish); // While statement to continuee till 3 correct words
		//     Increment the number of simiulations ran counter
		++simulation;
		// Ask the recruit if they would like to run the simulation again
		cout << "====================================================================================================================\n"; // Spacing
		cout << "\nWould you like to run the simulation again? Y/N: "; // Ask user to play again
		cin >> again; // record user input
	} while (again == 'Y'); // If the recruit wants to run the simulation again

	//     Display End of Simulations to the recruit
	cout << "Thank you for participating in Code Breaker Training Simulation.\n ";
	cout << "Ending Simulation...\n\n";

	//     Pause the Simulation with press any key to continue
	system("pause");

	return 0;
} // Ending the main function
