
# Number Guessing Game in C 🎮

A simple, interactive command-line number guessing game written in C. The program generates a random number between 1 and 100, and the player has to guess it with the help of high/low hints.

## Features
- Generates a random number for every new game session using `<time.h>`.
- Tracks and displays the total number of attempts taken to guess the correct number.
- User-friendly feedback (`The Number is larger` / `Guess is a smaller number`).

## How to Run
1. Compile the C program using a C compiler (like GCC):
   ```bash
   gcc guessing_game.c -o guessing_game

```

2. Run the executable:
```bash
./guessing_game

```



## Developed By

* **Ayush Mondal**

```

---

### Line-by-Line Meaning of Your C Code

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

```

* **Includes standard header files:**
* `<stdio.h>` enables standard input/output functions like `printf` and `scanf`.
* `<stdlib.h>` provides functions involving memory allocation, process control, and pseudo-random number generation (`rand`, `srand`).
* `<time.h>` gives access to time-related functions used to seed the random number generator.



```c
int main() {
    int random, guess;
    int no_of_guess = 0;
    srand(time(NULL));

```

* `int main()`: The entry point where C program execution begins.
* `int random, guess;`: Declares integer variables to store the target random number and the user's input.
* `int no_of_guess = 0;`: Initializes a counter to keep track of how many attempts the player makes.
* `srand(time(NULL));`: Seeds the random number generator using the current system time, ensuring a different random number is generated every time the program runs.

```c
    printf("Wellcome to the world of Gusseng game\n");
    random = rand() % 100 + 1; //generating between 0 to 100

```

* `printf(...)`: Prints a welcome message to the console.
* `random = rand() % 100 + 1;`: Generates a pseudo-random number. `rand() % 100` restricts values from 0 to 99, and adding `1` shifts the range to **1 through 100**.

```c
    do{
        printf("Please enter your Guess between(1 to 100): ");
        scanf("%d", &guess);
        no_of_guess++;

```

* `do { ... } while(...)`: A loop that executes at least once and continues running until the user guesses the correct number.
* `scanf(...)`: Reads the integer entered by the user and stores it in the `guess` variable.
* `no_of_guess++;`: Increments the attempt counter by 1 with each loop iteration.

```c
        if(guess < random){
            printf("The Number is larger.\n");
        }else if(guess > random){
            printf("Guess is a smaller number\n");
        }else {
            printf("Congratulations  !!!  You have successfully guessed the Number in %d attempts.", no_of_guess);
        }
    }while(guess != random);

```

* **Conditional Logic (`if-else`):**
* If the user's guess is **less** than the target number, it prompts them that the target number is larger.
* If the user's guess is **greater** than the target number, it informs them that the target number is smaller.
* If it matches, it congratulates the user and displays the total number of attempts.


* `while(guess != random);`: Repeats the loop as long as the user's guess does not match the secret number.

```c
    printf("\n Bye Bye, Thanks for paying");
    printf("\nDeveloped By: Ayush Mondal");
    return 0;
}

```

* Prints a farewell message and developer credit once the game concludes.
* `return 0;`: Signals to the operating system that the program executed successfully.


Here is a clean and professional `README.md` file for your Tic-Tac-Toe game repository, followed by a line-by-line explanation of your C code.

---

### README.md Content

```markdown
# Tic-Tac-Toe Game in C ❌⭕

A terminal-based, interactive Tic-Tac-Toe game written in C featuring a built-in scoreboard and two AI difficulty levels (Human & GOD mode).

## Features
- **Two Difficulty Levels:**
  - **Human (Standard):** Standard moves and basic strategy.
  - **GOD (Impossible to Win):** Advanced AI heuristic strategy designed to block wins and control the board.
- **Scoreboard Tracking:** Keeps track of Player X wins, Computer wins, Draws, and total games played.
- **Dynamic Turn Assignment:** Randomly decides who goes first at the start of every match.
- **Cross-Platform Screen Refresh:** Clears the console screen smoothly across different operating systems (`Windows` and `Linux/macOS`).

## How to Run
1. Compile the C program using a C compiler (like GCC):
   ```bash
   gcc tictactoe.c -o tictactoe

```

2. Run the executable:
```bash
./tictactoe

```



## Developed By

* **Ayush Mondal**

```

---

# Tic-Tac-Toe game
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define max 3
#define X 'x'
#define O 'o'

```

* **Preprocessor Directives & Constants:**
* `#define max 3`: Defines the grid size for the $3 \times 3$ board.
* `#define X 'x'` and `#define O 'o'`: Sets constant symbols representing the Player and the Computer markers.



```c
typedef struct{
    int player;
    int computer; 
    int draw;
    int no_playing;
} Score;

int difficulty;
Score score = {.player = 0, .computer = 0, .draw = 0, .no_playing = 0};

```

* **Structure and Global Variables:**
* `Score`: A custom data structure to hold game statistics (player wins, computer wins, draws, and total games played).
* `difficulty`: Tracks the selected game mode (Human vs. GOD).
* `score`: Initializes the scoreboard counters to `0`.



```c
void input_difficulty(){
    while(1){
        printf("\n======= Tic-Tac-Toe Game =======");
        printf("\nSelect difficulty level:\n");
        printf("\n1. HUMAN (standard). \n2. GOD (Impossible to Win). \n3. Exit.\n");
        printf("\nEnter your Choice: ");
        scanf("%d", &difficulty);
        if (difficulty !=1 && difficulty !=2 && difficulty != 3){
            printf("\nIncorrect choice enter (1/2/3) !!\n");
        }else if(difficulty == 3){
            printf("\n.....Goodby.....\n");
            exit(0);
        }else {
            break;
        }
    };
}

```

* **`input_difficulty()`**: Displays a menu allowing the user to select the game difficulty or exit the application. Validates user input in an infinite loop until a correct choice is made.

```c
void clear_screen(){
    #ifdef _WIN32
        system("cls");
    #else
        system("clear");
    #endif
}

```

* **`clear_screen()`**: Uses conditional compilation to check the operating system. It runs `cls` for Windows and `clear` for Unix/Linux/macOS to refresh the terminal view.

```c
void print_board(char board[max][max]){
    clear_screen();
    printf("\nScore Board \n1. Player X: %d \n2. Computer: %d \n3. Draws: %d\n4. No of Playing: %d\n",score.player,score.computer,score.draw,score.no_playing);
    printf("\n---- Tic-Tac-Toe Game ----\n");
    for(int i = 0; i < max; i++){
        printf("\n");
        for(int j = 0; j < max; j++){
            printf(" %c ",board[i][j]);
            if(j < max - 1){
                printf("|");
            }
        } 
        if(i < max - 1){
            printf("\n---+---+---");
        }
    }
    printf("\n\n");
}

```

* **`print_board()`**: Clears the console, prints the live scoreboard statistics, and formats the $3 \times 3$ grid using text borders (`|` and `---+---+---`).

```c
int check_win(char board[max][max], char player){
    for(int i = 0; i < max; i++){
        if(board[i][0] == player && board[i][1] == player && board[i][2] == player){
            return 1;
        } if(board[0][i] == player && board[1][i] == player && board[2][i] == player ){
            return 1;
        }
    }
    if((board[0][0]== player && board[1][1]== player &&board[2][2]== player)){
        return 1;
    } if(board[2][0]== player && board[1][1]== player &&board[0][2]== player){
        return 1;
    }
    return 0;
}

```

* **`check_win()`**: Checks all winning combinations (horizontal rows, vertical columns, and both diagonals) to see if a specified player (`X` or `O`) has won. Returns `1` if a win condition is met, otherwise `0`.

```c
int check_draw(char board[max][max]){
    for(int i = 0; i < max; i++){
        for(int j = 0;j < max; j++){
            if(board[i][j] == ' '){
                return 0;
            }
        }
    }
    return 1;
}

```

* **`check_draw()`**: Scans the board for any remaining empty spaces (`' '`). If no empty spaces are found and no one has won, it returns `1` (indicating a draw).

```c
int is_valid_move(char board[max][max],int row, int col) {
    return !(row < 0 || col < 0 || 
            row > 2 || col > 2  || 
            board[row][col]!= ' ');
}

```

* **`is_valid_move()`**: Validates if the player's coordinate choice falls within the allowed grid range ($0$ to $2$) and targets an empty spot.

```c
void player_move(char board[max][max]){
    int row, col;
    do {
        printf("\nPlayer X's turn.");
        printf("\nEnter row and column (1-3) for X: ");
        scanf("%d %d", &row, &col);
        row--;
        col--;
    } while (!is_valid_move(board, row, col));
    board[row][col] =X;
}

```

* **`player_move()`**: Prompts the user to input row and column numbers ($1$ to $3$). It subtracts `1` to align with 0-indexed arrays, validates the input, and places an `X` on the board.

```c
void computer_move(char board[max][max]){

    // 1. Play for immediate win
    for(int i = 0; i < max; i++){
        for(int j = 0; j < max; j++){
            if(board[i][j] == ' '){
                board[i][j] = O;
                if(check_win(board, O)){
                    return;
                }
                board[i][j] = ' ';
            }
        }
    }

    // 2. Block player's immediate win
    for(int i = 0; i < max; i++){
        for(int j = 0; j < max; j++){
            if(board[i][j] == ' '){
                board[i][j] = X;
                if(check_win(board, X)){
                    board[i][j] = O;
                    return;
                }
                board[i][j] = ' ';
            }
        }
    }

    // 3. GOD Mode Strategy
    if(difficulty == 2){
        // Play center, opposite corners, or available corners...
    }

    // 4. Play first available move
    for(int i = 0; i < max; i++){
        for(int j = 0; j < max; j++){
            if(board[i][j] == ' '){
                board[i][j] = O;
                return;
            }
        }
    }
}

```

* **`computer_move()`**: Contains the AI decision-making logic:
1. Checks if the computer can win in the next move.
2. Blocks the player if they are about to win.
3. Executes strategic tactical patterns (like targeting the center or corners) if **GOD mode** is active.
4. Falls back to the first available empty cell.



```c
void play_game(){
    score.no_playing++;
    char board[max][max]={
        {' ',' ',' '},
        {' ',' ',' '},
        {' ',' ',' '},
    };
    print_board(board);
    char current_player =  rand() % 2 == 0 ? X : O;
    while (1){
        if (current_player == X){
            print_board(board);
            player_move(board);
            if (check_win(board, X)){
                score.player++;
                print_board(board);
                printf("Congratulation You have won the match.");
                break;
            }
            current_player =O;
        } else {
            computer_move(board);
            print_board(board);
            if (check_win(board, O)){
                score.computer++;
                print_board(board);
                printf("I won...!!!\nBut you played well....");
                break;
            }
            current_player = X;
        }
        if (check_draw(board)){
            score.draw++;
            print_board(board);
            printf("\nIts a draw.....");
            break;
        }
    }
}

```

* **`play_game()`**: Manages a single round of the game: initializes an empty board, increments the total match counter, randomly determines who goes first, and loops back and forth between player and computer turns until a win or draw condition occurs, updating the scoreboard accordingly.

```c
int main() {
    srand(time(NULL));
    int choice;
    input_difficulty();
    do {
        play_game();
        printf("\nDo You want to play again ? (1 for yes and 0 for no): ");
        scanf("%d", &choice);
    } while(choice == 1);
    printf("Bye Bye, Thanks for Playing......");
    return 0;
}

```

* **`main()`**: The execution starting point. Seeds random numbers, calls the difficulty selector menu, and runs a loop that allows users to replay multiple rounds of Tic-Tac-Toe until they choose to exit.
