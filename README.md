# Minesweeper
A console application minesweeper game
using System;

static class Program
{
	
	static void NewGame(ref bool multiPlayermode,ref int[] hiddenValues)
	{
		Console.WriteLine();
		Console.WriteLine();
		Console.WriteLine("Welcome to Noah's Game of Mindsweeper!");
		Console.WriteLine();
		Console.Write("Do you require a short introduction to the rules? (Type 'yes' to see rules): ");
	
		string reply= Console.ReadLine();
		reply=reply.ToLower();
		if(reply == "yes")
			ShowInstructions();
		bool input = false;
		string playerNumber = "1";
		Console.Write("How many players (1 or 2)? ");
		playerNumber = Console.ReadLine();
		if(playerNumber == "1"|| playerNumber == "2")
		input = true;
		while(!input)
		{
			Console.WriteLine(" Input not valid, please enter 1 or 2: ");
			Console.Write("How many players (1 or 2)? ");
			playerNumber = Console.ReadLine();
			if(playerNumber == "1"|| playerNumber == "2")
			input = true;
		}
		if (playerNumber == "2")
			multiPlayermode = true;
		Console.WriteLine("Hit enter to proceed to game");
		Console.ReadLine();
		
		
		int tempNumber;
		Random rGen = new Random();
		for(int j = 0; j< 100; j++)
		{
			hiddenValues[j]=0;
		}
		for(int i = 0; i<16;)
		{
			tempNumber = rGen.Next(0,99);
			if(hiddenValues[tempNumber] != -1)
			{
				hiddenValues[tempNumber] = -1;
				i=i+1;
			}
		}

	}
	
	static void ShowInstructions()
	{
		Console.WriteLine("Welcome to my game of Minesweeper  (Hit enter to Continue)");
		Console.ReadLine();
		Console.WriteLine("The Rules to this game are very simple:");
		Console.ReadLine();
		Console.WriteLine("There are 15 bombs placed randomly throughout the game board, selecting a bomb will result in the game ending as a loss");
		Console.ReadLine();
		Console.WriteLine("Each move that is not a bomb, will provide you information about the bombs in its immediate vicinity");
		Console.ReadLine();
		Console.WriteLine("The number in the square, represents the number of bombs that that position is touching (above below, beside or to the diagnol)");
		Console.ReadLine();
		Console.WriteLine("To select a move, type the number corresponding to the square that you want to select:");
		Console.ReadLine();
		Console.WriteLine("Ex: 47 represents row 4, column 7");
		Console.ReadLine();
		Console.WriteLine("To place down/remove a 'flag'/marker as to where you think a bomb is, type in * and hit enter");
		Console.ReadLine();
		Console.WriteLine("Proceed to type in a position on the board to place down a marker there");
		Console.ReadLine();
		Console.WriteLine("If you successfully unvail all 85 squares without bombs, you win!");
		Console.ReadLine();
		Console.WriteLine("In two player mode, the players alternate moves until one player makes a mistake:");
		Console.ReadLine();
		Console.WriteLine("GOOD LUCK");
	}
	
	static void HiddenValueMaker(ref int[] hiddenValues)
	{
		int closeBombs;
		for(int i =0; i <100;i++)
		{
			closeBombs = 0;
			if(hiddenValues[i] !=-1)
			{
				if(i == 0)
				{
					if(hiddenValues[1] == -1) closeBombs++;
					if(hiddenValues[10] == -1) closeBombs++;
					if(hiddenValues[11] == -1) closeBombs++;
				}
				else if(i == 9)
				{
					if(hiddenValues[8] == -1) closeBombs++;
					if(hiddenValues[18] == -1) closeBombs++;
					if(hiddenValues[19] == -1) closeBombs++;
				}
				else
				{
					if(i == 90)
					{
						if(hiddenValues[80] == -1) closeBombs++;
						if(hiddenValues[81] == -1) closeBombs++;
						if(hiddenValues[91] == -1) closeBombs++;
					}
					else if(i == 99)
					{
						if(hiddenValues[98] == -1) closeBombs++;
						if(hiddenValues[88] == -1) closeBombs++;
						if(hiddenValues[89] == -1) closeBombs++;
					}
					else
					{
						if(i%10 ==0)
						{
							if(hiddenValues[i-10] == -1) closeBombs++;
							if(hiddenValues[i+10] == -1) closeBombs++;
							if(hiddenValues[i-9] == -1) closeBombs++;
							if(hiddenValues[i+1] == -1) closeBombs++;
							if(hiddenValues[i+11] == -1) closeBombs++;
						}
						else if(i%10==9)
						{
							if(hiddenValues[i-10] == -1) closeBombs++;
							if(hiddenValues[i+10] == -1) closeBombs++;
							if(hiddenValues[i+9] == -1) closeBombs++;
							if(hiddenValues[i-1] == -1) closeBombs++;
							if(hiddenValues[i-11] == -1) closeBombs++;
						}
						else
						{
							if(i<10)
							{
								if(hiddenValues[i-1] == -1) closeBombs++;
								if(hiddenValues[i+1] == -1) closeBombs++;
								if(hiddenValues[i+9] == -1) closeBombs++;
								if(hiddenValues[i+10] == -1) closeBombs++;
								if(hiddenValues[i+11] == -1) closeBombs++;
							}
							else if(i>90)
							{
								if(hiddenValues[i-1] == -1) closeBombs++;
								if(hiddenValues[i+1] == -1) closeBombs++;
								if(hiddenValues[i-9] == -1) closeBombs++;
								if(hiddenValues[i-10] == -1) closeBombs++;
								if(hiddenValues[i-11] == -1) closeBombs++;
							}
							else
							{
								if(hiddenValues[i-1] == -1) closeBombs++;
								if(hiddenValues[i+1] == -1) closeBombs++;
								if(hiddenValues[i-9] == -1) closeBombs++;
								if(hiddenValues[i-10] == -1) closeBombs++;
								if(hiddenValues[i-11] == -1) closeBombs++;
								if(hiddenValues[i+9] == -1) closeBombs++;
								if(hiddenValues[i+10] == -1) closeBombs++;
								if(hiddenValues[i+11] == -1) closeBombs++;
							}
						}
					}
				}
			
			}
			if(hiddenValues[i] !=-1)
				hiddenValues[i] = closeBombs;
		}
		
		
	}
	static void ShowFullBoard(int [] hiddenValues)
	{
		Console.WriteLine("Here is the actual Final Board:");
		Console.WriteLine("         0   1   2   3   4   5   6   7   8   9    <--- Second Digit");
		Console.WriteLine("  ______________________________________________");
		for(int i = 0; i < 100; i++)
		{
			if(i%10 == 0)
			{
				if(i!=0){
				Console.Write("|");
				Console.WriteLine();
				}
				if(i == 0)
				{
					Console.Write("Row {0}  ", i);
				}
				if(i!=0)
				{
					Console.WriteLine("      _________________________________________");
					Console.Write("Row {0} ", i);
				}
			}

				
				if(hiddenValues[i] !=0)
					if(hiddenValues[i] !=-1)
						Console.Write("| {0} ", hiddenValues[i]);
					else
						Console.Write("| * ", hiddenValues[i]);
				else
					Console.Write("|   ");
			
				
		}
		Console.WriteLine("|");
		
	}
	static void ShowBoard(int [] hiddenValues, bool [] isShown, bool [] isMarked)
	{
		Console.WriteLine();
		Console.WriteLine("        0   1   2   3   4   5   6   7   8   9    <--- Second Digit");
		Console.WriteLine("________________________________________________");
		for(int i = 0; i < 100; i++)
		{
			if(i%10 == 0)
			{
				if(i!=0)
				{
				Console.Write("|");
				Console.WriteLine();
				}
				if(i == 0)
				{
					Console.Write("Row {0} ", i);
				}
				if(i!=0)
				{
					Console.WriteLine("      _________________________________________");
					Console.Write("Row {0}", i);
				}
			}
			if(isShown[i] == true )
			{
				if(hiddenValues[i] !=-1)
					Console.Write("| {0} ", hiddenValues[i]);
				
				else
					Console.Write("|bomb");
			}
			else if (isMarked[i] == true)
				{
					
					Console.Write("| * ");
				}
			else
				Console.Write("|   ");
				
		}
		Console.WriteLine("|");
		Console.WriteLine("      _________________________________________");
		Console.WriteLine("");
	}
	static void EnterMove(bool multiPlayerMode,ref int player,ref int [] hiddenValues, ref bool [] isShown, ref bool [] isMarked, ref bool isLoser, ref bool isWinner, ref int lastMove)
	{
		bool validMove = false;
		int movePosition;
		string word;
		bool markMode = false;
		while(!validMove)
		{
			validMove=true;
			if(multiPlayerMode)
				Console.Write("Player {0}, please enter move: ", player+1);
			else
				Console.Write("Please enter move: ");
			word = Console.ReadLine();
			if(word == "*")
			{
				markMode=true;
				Console.Write("Please Enter Space to Mark:");
				word = Console.ReadLine();
			}
			else
				Console.WriteLine();
			validMove = int.TryParse(word, out movePosition);
			if(!validMove)
				Console.WriteLine("  Please Enter a number between 0 and 99");
			else
			{
				if(movePosition < 0||movePosition > 99)
				{
					validMove = false;
					Console.WriteLine("  Please Enter a number between 0 and 99");
				}
				else if (isShown[movePosition] == true)
				{
					validMove = false;
					Console.WriteLine("Please choose a space that has not already been selected:");
				}
				else
				{
					if(markMode==true)
					{
						if(isMarked[movePosition] == true)
							isMarked[movePosition] = false;
						else
							isMarked[movePosition] = true;
					}
					else
					{
						lastMove = movePosition;
						isShown[movePosition] = true;
						if(hiddenValues[movePosition] == 0)
							BlowUp(hiddenValues, ref isShown, movePosition);
						if(multiPlayerMode==true)
							player = (player +1)%2;
						if(hiddenValues[movePosition] == -1)
						{
							isLoser = true;
							return;
						}
					}
				
				}
			}
		}
	
		int numberOfSelectedSpaces = 0;
		for(int i = 0; i < 100; i++ )
		{
			if(isShown[i] == true)
			{
				numberOfSelectedSpaces++;
			}
		}
		if(numberOfSelectedSpaces >= 85)
		{
			isWinner = true;
			return;
		}
		return;
		
	}
	static void endGame(bool multiPlayerMode, int player, bool isWinner, int [] hiddenValues, int lastMove)
	{
		
		if(isWinner)
		{
			Console.WriteLine();
			Console.WriteLine("Congrats you won!!!!!!!!!!! :) :)");
		}
		else
		{
			ShowFullBoard(hiddenValues);
			Console.WriteLine();
			if(!multiPlayerMode)
				Console.WriteLine("Sorry There was a bomb at position {0}! better luck next time!!!", lastMove);
			else if(player == 1)
			{
				Console.WriteLine("Sorry Player 1, there was a bomb at position {0}, you lose!", lastMove);
				Console.WriteLine();
				Console.WriteLine("Congratulations Player 2, you win!");
			}
			else
			{
				Console.WriteLine("Sorry player 2, there was a bomb at position {0}, you lose!", lastMove);
				Console.WriteLine();
				Console.WriteLine("Congratulations Player 1, you win!");
			}
		}
		Console.ReadLine();
		return;
	}
	
	static void BlowUp(int [] hiddenValues, ref bool [] isShown, int position)
	{
		int numberToBeBlownUp = 1;
		int [] blownUpSquares = new int[100];
		bool [] alreadyBlownUp = new bool [100];
		blownUpSquares[0] = position;
		for(int i = 0; i < numberToBeBlownUp; i++)
		
		{
			Console.WriteLine(numberToBeBlownUp);
		if(alreadyBlownUp[blownUpSquares[i]] == false){
			Console.WriteLine(blownUpSquares[i]);
			if(blownUpSquares[i] == 0)
				{
					Console.WriteLine("GFGDFSGEFSDWDSF");
				}
			if(blownUpSquares[i]<90)
			{
				isShown[blownUpSquares[i] +10] = true;
				if(blownUpSquares[i]%10 != 0)
					isShown[blownUpSquares[i] + 9] = true;
				if(hiddenValues[blownUpSquares[i] + 10] == 0)
				{
					if(alreadyBlownUp[blownUpSquares[i] + 10] == false)
					{
						Console.WriteLine("Below");
						
						blownUpSquares[numberToBeBlownUp] = blownUpSquares[i] + 10;
						numberToBeBlownUp++;
						isShown[blownUpSquares[i] +10] = true;
						alreadyBlownUp[blownUpSquares[i]] = true;
					}
				}
			}
			if(blownUpSquares[i]>9)
			{
				if(blownUpSquares[i]%10 != 0)
					isShown[blownUpSquares[i] - 11] = true;
				isShown[blownUpSquares[i] -10] = true;
				if(hiddenValues[blownUpSquares[i] - 10] == 0)
				{
					if(alreadyBlownUp[blownUpSquares[i] - 10] == false)
					{
						Console.WriteLine("Below");
						
						blownUpSquares[numberToBeBlownUp] = blownUpSquares[i] - 10;
						numberToBeBlownUp++;
						isShown[blownUpSquares[i] -10] = true;
						alreadyBlownUp[blownUpSquares[i]] = true;
					}
				}
			}
			if(blownUpSquares[i]%10!=0)
			{
				isShown[blownUpSquares[i] -1] = true;
				if(hiddenValues[blownUpSquares[i] - 1] == 0)
				{
					if(alreadyBlownUp[blownUpSquares[i] - 1] == false)
					{
						Console.WriteLine("Below");
						
						blownUpSquares[numberToBeBlownUp] = blownUpSquares[i] - 1;
						numberToBeBlownUp++;
						isShown[blownUpSquares[i] -1] = true;
						alreadyBlownUp[blownUpSquares[i]] = true;
					}
				}
			}
			if((blownUpSquares[i] + 1)%10!=0)
			{
				if(blownUpSquares[i]<90)
					isShown[blownUpSquares[i] + 11] = true;
				if(blownUpSquares[i]>9)
					isShown[blownUpSquares[i] - 9] = true;
				isShown[blownUpSquares[i] +1] = true;
				if(hiddenValues[blownUpSquares[i] + 1] == 0)
				{
					if(alreadyBlownUp[blownUpSquares[i] + 1] == false)
					{
						Console.WriteLine("Below");
						
						blownUpSquares[numberToBeBlownUp] = blownUpSquares[i] + 1;
						numberToBeBlownUp++;
						isShown[blownUpSquares[i] +1] = true;
						alreadyBlownUp[blownUpSquares[i]] = true;
					}
				}
			}
			
			isShown[blownUpSquares[i]] = true;
			}
		}
	}
	static void Main()
	{
		int[]hiddenValues = new int [100];
		bool[]isShown = new bool [100];
		bool[]isMarked = new bool [100];
		int player = 0;
		int lastMove = 0;
		bool multiPlayerMode = false;
		NewGame(ref multiPlayerMode,ref hiddenValues);
		HiddenValueMaker(ref hiddenValues);
		bool isLoser = false;
		bool isWinner = false;
		ShowBoard(hiddenValues, isShown, isMarked);
		
		while(!isLoser&&!isWinner)
		{
			EnterMove(multiPlayerMode,ref player, ref hiddenValues, ref isShown, ref isMarked, ref isLoser, ref isWinner, ref lastMove);
			ShowBoard(hiddenValues, isShown, isMarked);
		}
		endGame(multiPlayerMode, player,isWinner, hiddenValues, lastMove);
		
	}	
}
