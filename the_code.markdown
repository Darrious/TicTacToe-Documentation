---
layout: page
title: Code
permalink: /Code/
nav_order: 5
---

# Code

### <span style="color:grey"> Table of contents </span>
1. [main() method](#main)
2. [setup() function](#setup)
3. [The game loop](#game)
	1. [draw() function](#draw)
	2. [input() function](#input)
	3. [testGame() function](#test)

---

## main() method <a name="main"></a>

`TicTacToe.cpp` only has one method which is the main method. First, we declare some variables including an instance of `Computer.h` and `Game.h`. 


	// Ends game if true
    bool gameOver = false;
    int quit;
    int choice;

	//Class for player v player
    Game test;
	//Class for player v AI
    Computer ai;


The user is prompted to select between playing against AI or another player.


	cout << "AI (1) or 2 player (2)" << endl;
	cin >> choice;

This selection lets us know which class to use (`Game.h` vs `Computer.h`). It will call the `setup()` function and then enter the game loop. This section of code is nearly indentical for `choice == 1` and `choice == 2`. 

	if(choice == 2){
		
        // Sets up initial values
        test.setup();

        // Game loop
        while(quit != 99){
            cout << "Press 1 and enter to play, press 99 to quit" << endl;
            cin >> quit;

            while(gameOver != true){
                test.draw();
                test.input();
                gameOver = test.testGame();
            }

            gameOver = false;
            test.reset();
        }
    }


	cout << "AI (1) or 2 player (2)" << endl;
	cin >> choice;

---

## setup() function <a name="main"></a>

Before we enter the game loop, we call the `Game.h` `setup()` function.

	void setup(){
        gameOver = false;
        one = "7";
        two = "8";
        three = "9";
        four = "4";
        five = "5";
        six = "6";
        seven = "1";
        eight = "2";
        nine = "3";
        for(int i = 0; i < 9; i++){
            boardCheck[i] = 0;
        }
        p1Score = 0;
        p2Score = 0;

        cout << "-Tic-Tac-Toe- Tips" << endl;
        cout << "*Use the number pad to select a square\n";
        cout << "*P1 is X, P2 is O" << endl << endl;
    }

This function gets some of our variables set up and also initializes the `boardcheck` array. This array will check if there are three in a row. Some information is also sent to the user such as how to make a selection on the board.

---

## The game loop <a name="game"></a>

The game loop consists of two loops. The outer loop is the main menu. When a selection is made, we enter the inner loop. The inner look only stops when `gameOver = true`. The outer loop only stops when the user enters 99. When the outer loop is broken, the program terminates 

	// Game loop
    while(quit != 99){
        cout << "Press 1 and enter to play, press 99 to quit" << endl;
        cin >> quit;

        while(gameOver != true){
            test.draw();
            test.input();
            gameOver = test.testGame();
        }

        gameOver = false;
        test.reset();
    }


Taking a look at the inner loop, we can see that a few functions are called on the `Game.h` class.

	while(gameOver != true){
	    test.draw();
	    test.input();
	    gameOver = test.testGame();
    }

---

## draw() function <a name="draw"></a>

`draw()` is used to display the game board. We use the numerical variables we defined earlier in the `setUp()` function.

	void draw(){
        system("cls");
        cout << "-Tic-Tac-Toe-          Tip:" << endl;
        cout << "Score(2+ per game)     Use the number pad to select a square" << endl;
        cout << "P1 - " << p1Score << " P2 - " << p2Score << endl;
        cout << "+---+---+---+" << endl;
        cout << "| " << one << " | " << two << " | " << three  << " |" << endl;
        cout << "+---+---+---+" << endl;
        cout << "| " << four << " | " << five << " | " << six << " |" << endl;
        cout << "+---+---+---+" << endl;
        cout << "| " << seven << " | " << eight << " | " << nine << " |" << endl;
        cout << "+---+---+---+" << endl << endl;
    }

---

## input() function <a name="input"></a>

The `input()` function asks for user input and then adds it to the board. After every move, `draw()` is called to update the board and `logic()` is called to determine if the player won the game on that move.



    switch(value){
        case 7: one = "X"; boardCheck[6] = 1; break;
        case 8: two = "X"; boardCheck[7] = 1; break;
        case 9: three = "X"; boardCheck[8] = 1; break;
        case 4: four = "X"; boardCheck[3] = 1; break;
        case 5: five = "X"; boardCheck[4] = 1; break;
        case 6: six = "X"; boardCheck[5] = 1; break;
        case 1: seven = "X"; boardCheck[0] = 1; break;
        case 2: eight = "X"; boardCheck[1] = 1; break;
        case 3: nine = "X"; boardCheck[2] = 1; break;
    }


This switch statement takes our input and assigns it to the appropriate board variable. The `boardCheck` array is used to see if that board location is taken. When we assign a board square, we assign 1 to `boardCheck` in that location.


	// Takes P1 input and replaces board piece
    cout << "It is P1 Turn:" << endl;
    cin >> value;

    // Loop to check for taken square
    while (boardCheck[value - 1] == 1){
        cout << "Square is already taken, try again:" << endl;
        cin >> value;
    }


---

## testGame() function <a name="test"></a>

The `testGame()` function is very simple. It checks if the boolean variable `gameOver` is true. In our game loop, if `gameOver == true` then the game ends.

	public:
    	bool testGame()
        	{ return gameOver; }

---

<sup><span style="color:grey">Copyright © 2020 Darrious Barger. Distributed by an [MIT license](https://opensource.org/licenses/MIT).</span></sup>