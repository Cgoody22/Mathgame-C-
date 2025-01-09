# Mathgame-C-
using System;

partial class Program {
    static Random rand = new Random();
    public static void Main(string[] args) {
        int gameDifficulty = 0;
        bool gameDifficultyValid = false; 
        Console.WriteLine("Welcome to The Math game.");
        Console.WriteLine("Please enter your name");
        string name = Console.ReadLine();
        while (name == "")
        {
            Console.WriteLine("Name is empty, try again.");
            Console.WriteLine("Please enter your name");
            name = Console.ReadLine(); 
        }

        Console.WriteLine("Which Difficulty would you like to play?");
        Console.WriteLine("Level 1 for Easy Mode Numbers 1-9");
        Console.WriteLine("Level 2 for Medium Mode Numbers 10-99");
        Console.WriteLine("Level 3 for Hard Mode Numbers 100-999");

        while (!gameDifficultyValid)
        {
            Console.WriteLine("Please enter your difficulty 1-3: ");
            string input = Console.ReadLine();

            if (int.TryParse(input, out gameDifficulty) && gameDifficulty >= 1 && gameDifficulty <= 3)
            {
                gameDifficultyValid = true; 
                Console.WriteLine($"You have selected {(gameDifficulty == 1 ? "Easy" : gameDifficulty == 2 ? "Medium" : "Hard")} Mode");
            }
            else
            {
                Console.WriteLine("Invalid Option Please choose from 1, 2, or 3");
            }
        }

        MathGameEngine(gameDifficulty);
    }

    static void MathGameEngine(int gameDifficulty)
    {
        int numQuestions = 0;
        bool questionsValid = false;
        Console.WriteLine("How many Questions would you like to answer from 3-10?");

        while (!questionsValid)
        {
            string input = Console.ReadLine();
            if (int.TryParse(input, out numQuestions) && numQuestions >= 3 && numQuestions <= 10)
            {
                Console.WriteLine($"You have selected {numQuestions} Questions");
                questionsValid = true;
            }
            else 
            {
                Console.WriteLine("Invalid Option Please choose from 3-10");
            }
        }

        int rightAnswers = 0;
        for (int i = 0; i < numQuestions; i++)
        {
            int num1 = numDifficulty(gameDifficulty);
            int num2 = numDifficulty(gameDifficulty);
            int correctAnswer = num1 + num2;
            Console.WriteLine($"Problem {i + 1}: {num1} + {num2} = ?");
            int attempts = 0;
            while (attempts < 3)
            {
                int userAnswer;
                if (int.TryParse(Console.ReadLine(), out userAnswer))
                {
                    if (userAnswer == correctAnswer)
                    {
                        Console.WriteLine("Yay! You got it right!!!");
                        rightAnswers++;
                        break;
                    }
                    else
                    {
                        Console.WriteLine("Oops! You got it wrong.");
                    }
                }
                else
                {
                    Console.WriteLine("Please enter a number.");
                }
                attempts++;
                if (attempts == 3)
                {
                    Console.WriteLine($"The correct answer was: {correctAnswer}");
                }
            }
        }

        double scorePercentage = rightAnswers / numQuestions * 100;
        Console.WriteLine($"Game Over! You answered {rightAnswers} out of {numQuestions} questions correctly ({scorePercentage:N2}%).");
    }

            static int numDifficulty(int difficulty) {
            switch (difficulty) {
                case 1:
                    return rand.Next(1, 10);
                case 2:
                    return rand.Next(10, 100);
                case 3:
                    return rand.Next(100, 999);
                default:
                    Console.WriteLine("Invalid game difficulty.");
                    return 0; 
            }
        }
    
}
