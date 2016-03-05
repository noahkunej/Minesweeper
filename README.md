# Minesweeper
A console application minesweeper game
using System;


static class Program
{
	
	static void NewGame(ref int[] hiddenValues)
	{
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
	static void showFullBoard(int [] hiddenValues)
	{
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
					Console.Write("Row {0} |", i);
				}
				if(i!=0)
				Console.Write("Row {0}|", i);
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
	static void showBoard(int [] hiddenValues, bool [] isShown)
	{
		Console.WriteLine("         0   1   2   3   4   5   6   7   8   9    <--- Second Digit");
		Console.WriteLine("  ______________________________________________");
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
					Console.Write("Row {0} |", i);
				}
				if(i!=0)
				Console.Write("Row {0}|", i);
			}
			if(isShown[i] == true )
			{
				Console.Write("  ______________________________________________");
				if(hiddenValues[i] !=0 && hiddenValues[i] !=-1)
					Console.Write("| {0} ", hiddenValues[i]);
				else if (hiddenValues[i] ==-1)
				{
					Console.Write("| B ");
				}
				else
					Console.Write("|     ");
			}
			else
				Console.Write("| X ");
				
		}
		Console.WriteLine("|");
		Console.WriteLine("");
		Console.WriteLine("");
	}
	
	static void Main()
	{
		int[]hiddenValues = new int [101];
		bool[]isShown = new bool [101];
		NewGame(ref hiddenValues);
		HiddenValueMaker(ref hiddenValues);
		bool gameDone = false;
		bool isWinner = false;
		// while(!gameDone)
		// {
			showBoard(hiddenValues, isShown);
			showFullBoard(hiddenValues);
			// enterMove();
			// isWinner = isWinnerMethod();
			// gameDone = isGameDone();
		// }
		// if(isWinner)
		// {
			// Console.WriteLine("Congrats you won!!!!!!!!!!! :) :)");
		// }
		// else
		// {
			// showFullBoard();
			// Console.WriteLine("Good try, better luck next time!!!");
		// }
		
		
		
		
		
	}
	
	
}
