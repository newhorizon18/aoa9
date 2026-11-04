#include <stdio.h>
#include <stdlib.h>

int n, pos[20], count = 0;

int safe(int row, int col) {
    for(int i = 0; i < row; i++) {
        if(pos[i] == col || abs(pos[i] - col) == abs(i - row))
            return 0;
    }
    return 1;
}

void solve(int row) {
    if(row == n) {
        printf("\nSolution %d:\n", ++count);

        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++)
                printf("%c ", pos[i] == j ? 'Q' : '.');
            printf("\n");
        }
        return;
    }

    for(int col = 0; col < n; col++) {
        if(safe(row, col)) {
            pos[row] = col;
            solve(row + 1);
        }
    }
}

int main() {
    printf("Enter number of queens: ");
    if(scanf("%d", &n) != 1 || n < 1 || n > 10) {
        printf("Enter a value from 1 to 10.\n");
        return 1;
    }

    solve(0);

    if(count == 0)
        printf("No solution found.\n");

    return 0;
}
