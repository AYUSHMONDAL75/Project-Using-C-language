
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
