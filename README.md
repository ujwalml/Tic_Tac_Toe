# Tic_Tac_Toe
This project enables us to play Tic Tac Toe with the computer.
package MACT;
import java.util.*;
class ttt2 
{
	static char[][] board;
	
	public ttt2()
	{
		board = new char[3][3];
		initia();
	}
	void initia()
	{
		for(int i=0;i<board.length;i++)
		{
			for(int j=0;j<board[i].length;j++)
			{
				board[i][j]= ' ';
			}
		}
	}
	static void disp()
	{
		for(int i=0;i<board.length;i++)
		{
			System.out.print(" | ");
			for(int j=0;j<board[i].length;j++)
			{
				System.out.print(board[i][j]+" | ");
			}
			System.out.println();
			if(i==2)
			{
				break;
			}
			System.out.println("--------------");
			
	    }
		
	}
	
	static void placing(int row,int col,char place)
	{
		if((row>=0&&row<=2)&&(col>=0&&col<=2))
		{
			board[row][col]=place;
		}
		else
			System.out.println("INVALID ROW AND COLUMN, TRY AGAIN!");
	}
	static boolean colwin()
	{
		for(int j=0;j<3;j++)
		{
			if(board[0][j]!=' ' && (board[0][j]==board[1][j])&&(board[1][j]==board[2][j]))
			{
				return true;
			}
		}
		return false;
	}
	static boolean rowwin()
	{
		for(int i=0;i<3;i++)
		{
			if(board[i][0]!=' ' && (board[i][0]==board[i][1])&&(board[i][1]==board[i][2]))
			{
				return true;
			}
		}
		return false;
	}
	static boolean diagwin()
	{
		if(board[0][0] != ' ' &&(board[0][0]==board[1][1]&&board[1][1]==board[2][2])||board[0][2] != ' ' && (board[0][2]==board[1][1]&&board[1][1]==board[2][0]))
		{
			return true;
		}
		else
			return false;
	}
	static boolean checkdraw()
	{
		for(int i=0;i<3;i++)
		{
			for(int j=0;j<3;j++)
			{
				if(board[i][j]==' ') 
				{
					return false;
				}
		
			}
		}
		return true;
	}
}
abstract class bothplayer//for code reusability
{
	String name;
	char mark;
	abstract void Move();//within a class, if a single method is an abstract,then its class must be abstract
	boolean validMove(int row, int col)
	{
		if((row>=0&&row<=2)&&(col>=0&&col<=2)) 
		{
			if(ttt2.board[row][col]==' ') 
			{
				return true;
			}
		}
		return false;
	}
}
	class Player extends bothplayer
	{
		
		Player(String name,char mark)
		{
			this.mark=mark;
			this.name=name;
		}
		void Move()
		{
			int row,col;
			Scanner read=new Scanner(System.in);
			do
			{
				System.out.println("Enter the row and col:");
			    row=read.nextInt();
			    col=read.nextInt();
			}
			while(!validMove(row,col));
			ttt2.placing(row, col, mark);
		}
	}
	class AiPlayer extends bothplayer
	{
		
		AiPlayer(String name,char mark)
		{
			this.mark=mark;
			this.name=name;
		}
		void Move()
		{
			int row,col;
			Scanner read=new Scanner(System.in);
			do
			{
				Random r=new Random();
				row=r.nextInt(3);//Generates random no from 0-2 for row
				col=r.nextInt(3);//Generates random no from 0-2 for column
			}
			while(!validMove(row,col));
			ttt2.placing(row, col, mark);
		}
	}
	

	
	public class Game1{
	public static void main(String[]args)
{
	ttt2 b=new ttt2();
	System.out.println("TIC TAC TOE\nLETS START!");
	Scanner sc=new Scanner(System.in);
	System.out.println("Enter the name of the Player1:");
	String Player1=sc.nextLine();

	
	Player p1 = new Player(Player1,'X');
	AiPlayer p2 = new AiPlayer("Computer",'O');
	bothplayer cp;
	cp=p1;
	for(;;)
	{
	System.out.println(cp.name + " 's turn. ");
	cp.Move();
	ttt2.disp();
	if(ttt2.rowwin()||ttt2.colwin()||ttt2.diagwin())
	{
		System.out.println(cp.name +" HAS WON!");
		break;
	}
	else if(ttt2.checkdraw())
	{
		System.out.println("GAME DRAW");
		break;
	}
	else
	{
		if(cp==p1)
		{
			cp=p2;
		}
		else
			cp=p1;
	}
}}}
