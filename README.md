
# Experiment No. 9 – 15-Puzzle Problem Using Greedy Method

**Created By:** Krish Mhatre

## C Program

```c
#include <stdio.h>
#define N 4

int a[N][N], goal[N][N];

int misplaced() {
    int count = 0;

    for(int i = 0; i < N; i++)
        for(int j = 0; j < N; j++)
            if(a[i][j] != 0 && a[i][j] != goal[i][j])
                count++;

    return count;
}

void show() {
    for(int i = 0; i < N; i++) {
        for(int j = 0; j < N; j++)
            printf("%2d ", a[i][j]);
        printf("\n");
    }
}

int main() {
    int dx[] = {-1, 1, 0, 0};
    int dy[] = {0, 0, -1, 1};

    printf("Enter initial 4x4 matrix (0 for blank):\n");
    for(int i = 0; i < N; i++)
        for(int j = 0; j < N; j++)
            scanf("%d", &a[i][j]);

    printf("Enter target 4x4 matrix:\n");
    for(int i = 0; i < N; i++)
        for(int j = 0; j < N; j++)
            scanf("%d", &goal[i][j]);

    for(int moves = 0; moves < 16; moves++) {
        int current = misplaced();

        if(current == 0) {
            printf("\nPuzzle solved in %d moves.\n", moves);
            return 0;
        }

        int x = -1, y = -1;

        for(int i = 0; i < N; i++)
            for(int j = 0; j < N; j++)
                if(a[i][j] == 0) {
                    x = i;
                    y = j;
                }

        if(x == -1) {
            printf("No blank tile found.\n");
            return 1;
        }

        int best = current, bx = -1, by = -1;

        for(int k = 0; k < 4; k++) {
            int nx = x + dx[k];
            int ny = y + dy[k];

            if(nx < 0 || nx >= N || ny < 0 || ny >= N)
                continue;

            a[x][y] = a[nx][ny];
            a[nx][ny] = 0;

            int score = misplaced();

            a[nx][ny] = a[x][y];
            a[x][y] = 0;

            if(score < best) {
                best = score;
                bx = nx;
                by = ny;
            }
        }

        if(bx == -1) {
            printf("\nNo better move found (local minimum).\n");
            return 0;
        }

        a[x][y] = a[bx][by];
        a[bx][by] = 0;

        printf("\nMove %d:\n", moves + 1);
        show();
    }

    return 0;
}
```

## Terminal Input (Copy and Paste)

After running the program, copy and paste this entire input into the terminal:

```text
1 2 3 4
5 6 0 8
9 10 7 11
13 14 15 12
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 0
```

## Output

```text
PS C:\AOA> gcc puzzle.c -o puzzle
PS C:\AOA> .\puzzle.exe

Enter initial 4x4 matrix (0 for blank):
1 2 3 4
5 6 0 8
9 10 7 11
13 14 15 12

Enter target 4x4 matrix:
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 0

Move 1:
 1  2  3  4
 5  6  7  8
 9 10  0 11
13 14 15 12

Move 2:
 1  2  3  4
 5  6  7  8
 9 10 11  0
13 14 15 12

Move 3:
 1  2  3  4
 5  6  7  8
 9 10 11 12
13 14 15  0

Puzzle solved in 3 moves.
```

## Aim
To implement the 15-Puzzle Problem using a Greedy Heuristic Method in C.

## Theory
The 15-Puzzle consists of a 4×4 board with 15 numbered tiles and one empty space.

The goal is to arrange the tiles in the correct order by moving tiles into the empty space.

The Greedy Method selects moves based on the number of misplaced tiles.

This simple method may stop at a local minimum and does not guarantee a solution for every puzzle.

## Algorithm
1. Start the program.
2. Enter the initial and target matrices.
3. Find the empty tile.
4. Count the misplaced tiles.
5. Check possible movements.
6. Choose a move that reduces misplaced tiles.
7. Repeat until solved or no better move exists.

## How to Run

**Step 1:** Save as `puzzle.c`.

**Step 2:** Compile:

```bash
gcc puzzle.c -o puzzle
```

**Step 3:** Run in PowerShell:

```powershell
.\puzzle.exe
```

**Step 4:** Copy the input from the Terminal Input section and paste it into the terminal.

## Time Complexity

- Per Move: O(N²)
- For M Moves: O(M × N²)
- Space Complexity: O(N²)

Where N = 4 for this puzzle.

## Conclusion
Successfully implemented the 15-Puzzle Problem using the Greedy Heuristic Method in C and solved the given example in three moves.
