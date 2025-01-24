# sudoko-game-dsa
#include <iostream>
using namespace std;
#define N 5

void printBoard(int board[N][N]) {
    for (int row = 0; row < N; row++) {
        for (int col = 0; col < N; col++)
            cout << board[row][col] << " ";
        cout << endl;
    }
}


bool isSafe(int board[N][N], int row, int col, int num) {
   
    for (int x = 0; x < N; x++) {
        if (board[row][x] == num || board[x][col] == num)
            return false;
    }
    return true;
}

bool solveSudoku(int board[N][N], int row, int col) {
 
    if (row == N)
        return true;


    if (col == N)
        return solveSudoku(board, row + 1, 0);


    if (board[row][col] != 0)
        return solveSudoku(board, row, col + 1);

    for (int num = 1; num <= N; num++) {
        if (isSafe(board, row, col, num)) {
            board[row][col] = num;
            if (solveSudoku(board, row, col + 1)){
                return true;
            }
            board[row][col] = 0;
        }
    }

    return false;
}

int main() {

    int board[N][N] = {
        {1, 0, 0, 0, 2},
        {0, 0, 3, 0, 0},
        {0, 1, 0, 0, 0},
        {0, 0, 0, 4, 0},
        {0, 4, 0, 0, 0}
    };

    if (solveSudoku(board, 0, 0)){
    cout<<" your completed sudoku is:"<<endl;
        printBoard(board);}
    else
        cout << " no solution exists." << endl;

    return 0;
}
