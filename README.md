# Minesweeper
A console application minesweeper game
 using System;
 
static class Program
{
	
	static void newGame(out int[] hiddenValues)
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
	
	static void showBoard(int [] hiddenValues, bool [] isShown)
	{
		Console.WriteLine("        0   1   2   3   4   5   6   7   8   9    <--- Second Digit");
		Console.WriteLine("  ______________________________________________");
		Console.WriteLine("  ______________________________________________");
		Console.WriteLine("                                          ");
		for(int i = 0; i <100; i++)
		{
			if(i%10 == 0)
			{
				Console.WriteLine("       |||" );
				Console.WriteLine("Row {0}|||", i);
				if(isShown[i] == true )
				{
					Console.Write("  ______________________________________________");
					if(hiddenValues[i] !=0)
						Console.Write("| {0} ", hiddenValues[i]);
					else
						Console.Write("|     ");
				}
			}
		}
	}
	static void Main()
	{
		int[]hiddenValues = new int [101];
		bool[]isShown = new bool [101];
		newGame(out hiddenValues);
		bool gameDone = false;
		bool isWinner = false;
		while(!gameDone)
		{
			showBoard(hiddenValues, isShown);
			// enterMove();
			// isWinner = isWinnerMethod();
			// gameDone = isGameDone();
		}
		// if(isWinner)
		// {
			// Console.WriteLine("Congrats you won!!!!!!!!!!! :) :)");
		// }
		// else
		// {
			// showWholeBoard();
			// Console.WriteLine("Good try, better luck next time!!!");
		// }
		
		
		
		
		
	}
	
	
}
