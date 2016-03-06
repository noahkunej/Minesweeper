# Minesweeper
A console application minesweeper game
using System;

static class Program
{
	
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
		Console.WriteLine("GOOD LUCK");
	}
	static void NewGame(ref int[] hiddenValues)
	{
		Console.WriteLine();
		Console.WriteLine();
		Console.WriteLine("             Welcome to Noah's Game of Mindsweeper!");
		Console.WriteLine();
		Console.WriteLine("Do you require a short introduction to the rules?");
	
		string reply= Console.ReadLine();
		reply=reply.ToLower();
		if(reply == "yes")
			ShowInstructions();
		Console.WriteLine("Hit enter to proceed to game");
		Console.ReadLine();
		
		
		int tempNumber;
		Random rGen = new Random();
		for(int j = 0; j< 100; j++)
		{
			hiddenValues[j]=0;
		}
		for(int i = 0; i<15;)
		{
			tempNumber = rGen.Next(0,99);
			if(hiddenValues[tempNumber] != -1)
			{
				hiddenValues[tempNumber] = -1;
				i=i+1;
			}
		}

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
	static void EnterMove(ref int [] hiddenValues, ref bool [] isShown, ref bool [] isMarked, ref bool isLoser, ref bool isWinner)
	{
		bool validMove = false;
		int movePosition;
		string word;
		bool markMode = false;
		while(!validMove)
		{
			validMove=true;
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
						isShown[movePosition] = true;
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
	static void endGame(bool isWinner, int [] hiddenValues)
	{
		if(isWinner)
		{
			Console.WriteLine("Congrats you won!!!!!!!!!!! :) :)");
		}
		else
		{
			ShowFullBoard(hiddenValues);
			Console.WriteLine("Sorry There was a bomb there! better luck next time!!!");
		}
		Console.ReadLine();
		return;
	}
	static void Main()
	{
		int[]hiddenValues = new int [100];
		bool[]isShown = new bool [100];
		bool[]isMarked = new bool [100];
		NewGame(ref hiddenValues);
		HiddenValueMaker(ref hiddenValues);
		bool isLoser = false;
		bool isWinner = false;
		ShowBoard(hiddenValues, isShown, isMarked);
		while(!isLoser&&!isWinner)
		{
			
			EnterMove(ref hiddenValues, ref isShown, ref isMarked, ref isLoser, ref isWinner);
			ShowBoard(hiddenValues, isShown, isMarked);
		}
		endGame(isWinner, hiddenValues);
		
	}	
}
