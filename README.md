# OIBSIP-JAVADEV-TASK2-NUMBERGUESSINGGAME-
NUMBER GUESSING GAME
TASK 2 · Number Guessing Game
Objective: Build a console or GUI-based game where the computer generates a random number and the user attempts to guess it, receiving higher/lower hints until correct.

Tech Stack: Java (console application or Swing GUI)

Feature Checklist:

[ ] System generates a random number in the range 1 to 100 at the start of each round
[ ] User is prompted to enter a guess (input via Scanner for console, or JTextField for GUI)
[ ] After each guess, display one of three responses: "Too High!", "Too Low!", or "Correct!"
[ ] Attempt counter visible to the user throughout the game
[ ] Maximum attempts limit (e.g., 7 attempts) — game ends with a "You Lost!" message if limit is reached, revealing the number
[ ] "Play Again" option after each round (yes/no prompt or button)
[ ] Score tracking across multiple rounds: display "Round X — guessed in Y attempts" summary
[ ] (Bonus) Difficulty levels: Easy (1–50, 10 attempts), Medium (1–100, 7 attempts), Hard (1–200, 5 attempts)


so lets code: 
import java.util.Random;
import java.util.Scanner;

class NumberGuessingGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        int minRange = 1;
        int maxRange = 100;
        int maxAttempts = 5;
        int score = 0;
        boolean playAgain = true;

        while (playAgain) {
            int targetNumber = random.nextInt(maxRange - minRange + 1) + minRange;
            int attempts = 0;
            boolean hasWon = false;

            System.out.println("Guess the number between " + minRange + " and " + maxRange + "!");

            while (attempts < maxAttempts) {
                System.out.print("Enter your guess: ");
                int userGuess = scanner.nextInt();
                attempts++;

                if (userGuess == targetNumber) {
                    System.out.println("Correct! You guessed it in " + attempts + " attempts.");
                    score += (maxAttempts - attempts + 1) * 10;
                    hasWon = true;
                    break;
                } else if (userGuess > targetNumber) {
                    System.out.println("Too high! Attempts left: " + (maxAttempts - attempts));
                } else {
                    System.out.println("Too low! Attempts left: " + (maxAttempts - attempts));
                }
            }

            if (!hasWon) {
                System.out.println("Out of attempts! The number was: " + targetNumber);
            }

            System.out.println("Current Score: " + score);
            System.out.print("Do you want to play again? (yes/no): ");
            String response = scanner.next();
            playAgain = response.equalsIgnoreCase("yes");
        }

        System.out.println("Game Over! Final Score: " + score);
        scanner.close();
    }
}
