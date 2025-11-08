```java
import java.util.Scanner;  
  
public class KnightsTour {  
  
    private final int[][] board;                              // the board, stores move numbers  
    private final int size = 5;                               // board size (5 for 5x5)  
    private final int[] moveX = {2, 1, -1, -2, -2, -1, 1, 2}; // knight moves x axis  
    private final int[] moveY = {1, 2, 2, 1, -1, -2, -2, -1}; // knight moves y axis  
  
    public KnightsTour() {  
        board = new int[size][size];  
        // initialize board to -1 (unvisited)  
        for (int i = 0; i < size; i++)  
            for (int j = 0; j < size; j++)  
                board[i][j] = -1;  
    }  
  
    // position on board unvisited  
    private boolean isVisited(int x, int y) {  
        return (x >= 0 && x < size && y >= 0 && y < size && board[x][y] == -1);  
    }  
  
    // it does what's on the tin  
    private void printBoard() {  
        for (int i = 0; i < size; i++) {  
            for (int j = 0; j < size; j++)  
                System.out.printf("%2d ", board[i][j]);  
            System.out.println();  
        }  
        System.out.println();  
    }  
  
    /**  
     * For the Tour of our lovely Knight, we're using     * Recursive DFS.     */    public boolean solve(int x, int y, int moveCount) {  
        board[x][y] = moveCount; // place knight  
  
        // i don't really know if you wanted it to be random or not,        // but i have given the option to place the knight down yourself or choose randomness  
        printBoard();  
  
        if (moveCount == size * size - 1) {  
            // all squares visited  
            return true;  
        }  
  
        // try all possible knight moves  
        for (int i = 0; i < 8; i++) {  
            int nextX = x + moveX[i];  
            int nextY = y + moveY[i];  
  
            if (isVisited(nextX, nextY)) {  
                if (solve(nextX, nextY, moveCount + 1)) {  
                    return true;  
                }  
            }  
        }  
  
        // backtracking  
        board[x][y] = -1;  
        return false;  
    }  
  
    public static void main(String[] args) {  
        Scanner sc = new Scanner(System.in);  
        int startX = 0, startY = 0;  
  
        KnightsTour kT = new KnightsTour();  
  
        System.out.println("Pick an option: (please make sure to use only integers, there is no bug safety here)\n0 - Random placement\n1 - Custom placement");  
        int option = sc.nextInt();  
  
        if (option == 0)  
            kT.solve((int) (Math.random() * 5), (int) (Math.random() * 5), 0);  
        else if (option == 1) {  
            System.out.print("Enter starting row (0-4): ");  
            startX = sc.nextInt();  
            System.out.print("Enter starting column (0-4): ");  
            startY = sc.nextInt();  
        }  
  
        if (kT.solve(startX, startY, 0)) {  
            System.out.println("Knight's Tour completed:");  
            kT.printBoard();  
        } else {  
            System.out.println("No solution found.");  
        }  
  
        sc.close();  
    }  
}
```