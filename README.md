# ProdigyInfoTechTask4
public class SudokuSolver {

    private static final int SIZE = 9; // size of the Sudoku grid

    public static void main(String[] args) {
        // Example unsolved Sudoku puzzle (0 represents empty cells)
        int[][] grid = {
            {5, 3, 0, 0, 7, 0, 0, 0, 0},
            {6, 0, 0, 1, 9, 5, 0, 0, 0},
            {0, 9, 8, 0, 0, 0, 0, 6, 0},
            {8, 0, 0, 0, 6, 0, 0, 0, 3},
            {4, 0, 0, 8, 0, 3, 0, 0, 1},
            {7, 0, 0, 0, 2, 0, 0, 0, 6},
            {0, 6, 0, 0, 0, 0, 2, 8, 0},
            {0, 0, 0, 4, 1, 9, 0, 0, 5},
            {0, 0, 0, 0, 8, 0, 0, 7, 9}
        };

        if (solveSudoku(grid)) {
            System.out.println("Sudoku solved successfully!");
            printGrid(grid);
        } else {
            System.out.println("Unsolvable Sudoku puzzle.");
        }
    }

    // Function to solve the Sudoku puzzle
    public static boolean solveSudoku(int[][] grid) {
        for (int row = 0; row < SIZE; row++) {
            for (int col = 0; col < SIZE; col++) {
                // Check if the current cell is empty (contains 0)
                if (grid[row][col] == 0) {
                    // Try placing digits 1 to 9 in the empty cell
                    for (int num = 1; num <= SIZE; num++) {
                        if (isSafe(grid, row, col, num)) {
                            grid[row][col] = num; // Place the number

                            // Recursively try to solve the rest of the grid
                            if (solveSudoku(grid)) {
                                return true;
                            }

                            // If placing the current number leads to an invalid solution,
                            // backtrack and try another number
                            grid[row][col] = 0;
                        }
                    }
                    // If no number from 1 to 9 can be placed in the current cell, return false
                    return false;
                }
            }
        }
        // If the entire grid is filled and no conflicts are found, return true
        return true;
    }

    // Function to check if placing a number in a specific cell is safe
    public static boolean isSafe(int[][] grid, int row, int col, int num) {
        // Check the row
        for (int x = 0; x < SIZE; x++) {
            if (grid[row][x] == num) {
                return false;
            }
        }

        // Check the column
        for (int x = 0; x < SIZE; x++) {
            if (grid[x][col] == num) {
                return false;
            }
        }

        // Check the 3x3 subgrid
        int startRow = row - row % 3;
        int startCol = col - col % 3;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (grid[i + startRow][j + startCol] == num) {
                    return false;
                }
            }
        }

        return true;
    }

    // Function to print the Sudoku grid
    public static void printGrid(int[][] grid) {
        for (int r = 0; r < SIZE; r++) {
            for (int d = 0; d < SIZE; d++) {
                System.out.print(grid[r][d]);
                System.out.print(" ");
            }
            System.out.print("\n");

            if ((r + 1) % 3 == 0 && r != SIZE - 1) {
                System.out.print("\n");
            }
        }
    }
}
