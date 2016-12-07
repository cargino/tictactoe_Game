# tictactoe_Game

//package ticTacToeGame;
import java.util.*;
//import javax.swing.JOptionPane; //optional
public class TicTacToe
{
	  public static final char PLAYER_X = 'X';
    public static final char PLAYER_O = 'O';
    private String xName;
    private String oName;
    private char board[];
    private int moveCount=0;//declaring instance variables
	public TicTacToe(String xName, String oName) 
	{
        this.xName=xName;
        this.oName=oName;
	}
    //this method intializes the one dimensional array called board to the charatcers '1', '2', '3',..'9'.
    //we are not using the index 0 of the array board
	public void initializeBoard()
	{
		 board=new char[]{'0','1','2','3','4','5','6','7','8','9'};
	}
    //this method allows the user to choose a location on the board
	public void takeATurn(Scanner keyboard, char player) {
        String name = "";
        int answerFromUser = 0;
        if (player == PLAYER_O)
            name = oName;
        if (player == PLAYER_X)
            name = xName;
        displayBoard();
        //JOptionPane.showInputDialog(name+" where would you like to play?");
        System.out.println(name + " where would you like to play? ");
        while (!keyboard.hasNextInt()){
            keyboard.next();
            System.out.println("Please enter a correct answer.");
        }
        answerFromUser = keyboard.nextInt();
        while (!validMove(answerFromUser)){
            System.out.println(answerFromUser + " is not a valid move.");
            System.out.println(name + " where would you like to play? ");
            answerFromUser = keyboard.nextInt();
         }
        board[answerFromUser]=player;
        moveCount++;
    }
    //This method will return true if player is a winner, false otherwise
	public boolean isWinner(char player)
	{
        if(player==board[1]&&player==board[2]&&player==board[3])
            return true;
        if(player==board[1]&&player==board[4]&&player==board[7])
            return true;
        if(player==board[3]&&player==board[6]&&player==board[9])
            return true;
        if(player==board[7]&&player==board[8]&&player==board[9])
            return true;
        if(player==board[1]&&player==board[5]&&player==board[9])
            return true;
        if(player==board[3]&&player==board[5]&&player==board[7])
            return true;
        if(player==board[2]&&player==board[5]&&player==board[8])
            return true;
        return false;
	}
	//Displays the result of the game
	public void displayResults()
	{
        if(isWinner(PLAYER_O))
            System.out.println("CONGRATULATIONS "+oName+" YOU WON!");
        else if(isWinner(PLAYER_X))
            System.out.println("CONGRATULATIONS "+xName+" YOU WON!");
        else if(moveCount==9)
            System.out.println("Nice Try! " +oName+" and "+xName+"! That was Cat Game.");
    }
	//checks to see if the position entered by the user is a valid position meaning that it must be \
    //between 1 and 9 and it must be a position that does not hold 'x' or 'o'
	private boolean validMove(int spot)
	{
        if((spot<1 || spot>9) || (board[spot]==PLAYER_O || board[spot]==PLAYER_X))
            return false;// I am only doing range validation here, input validation is in the driver
        return true;
	}
    //display the one imensional array board as a table.
	public void displayBoard ()
	{
		System.out.println(board[1]+" | "+board[2]+" | "+board[3]);
        System.out.println("---------");
        System.out.println(board[4]+" | "+board[5]+" | "+board[6]);
        System.out.println("---------");
        System.out.println(board[7]+" | "+board[8]+" | "+board[9]);
	}
}
