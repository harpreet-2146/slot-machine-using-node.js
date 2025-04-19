# slot-machine-using-node.js

This is a simple slot machine built using Node.js, following a tutorial by Tech With Tim. The program runs in the terminal and simulates a basic slot machine game.

I’m planning to upgrade this project by:
✅ Converting it into a web-based version using HTML, CSS, and JavaScript, so it runs in the browser instead of the terminal.
✅ Adding a better UI to make it more interactive and visually appealing.
✅ Implementing sound effects and animations for a more engaging experience.

🎯 Goal of the Game
You:

Deposit money

Choose how many lines to bet on (1 to 3)

Place a bet per line

Spin the slot machine (3x3 grid)

Win if all symbols in a line match

Continue playing until you run out or quit

🔌 First Part: User Input Functions
These functions use prompt-sync to get input from the terminal.

const prompt = require("prompt-sync")();
Loads the prompt-sync library so you can get user input in Node.js.

const deposit = () => { ... }
What it does:

Asks user to enter how much money they want to start with.

Loops until a valid number greater than 0 is entered.

🔍 Syntax notes:

parseFloat() → converts string input to a decimal number.

isNaN() → checks if the input is "Not a Number".

const getNumberOfLines = () => { ... }
Purpose:

Lets user choose 1, 2, or 3 lines to bet on.

Ensures they don’t enter anything invalid.

const getBet = (balance, lines) => { ... }
Purpose:

Asks how much to bet per line.

Ensures total bet (bet * lines) doesn’t exceed the current balance.

🎰 Slot Machine Core Logic
const SYMBOLS_COUNT & SYMBOL_VALUES

SYMBOLS_COUNT = { A: 2, B: 4, C: 6, D: 8 }
SYMBOL_VALUES = { A: 5, B: 4, C: 3, D: 2 }
These define how many of each symbol exist, and how valuable they are if you win with them.

So:

A is rare but worth the most

D is common and worth the least

This mimics real-life slot machine "rarity".

const spin = () => { ... }
What it does:

Creates a 3x3 slot machine grid (3 columns, 3 rows).

Randomly picks symbols for each column, based on how many of each are available.

🔍 How it works:
Make a giant array of all symbols:

['A', 'A', 'B', 'B', 'B', 'B', ..., 'D', 'D', ..., 'D']
For each column:

Make a copy of the symbol list

Randomly pick a symbol

Remove it from the list (so no repeats in the same column)

const transpose = (reels) => { ... }
Why needed:

spin() gives 3 columns of symbols.

But we want to check horizontal rows for matches.

This function rotates the grid so each row becomes an array we can check.

Example:

Before (columns):
[ [A,B,C], 
  [C,D,A],
  [A,A,B] ]

After (rows):
[ [A,C,A], 
  [B,D,A],
  [C,A,B] ]
const printRows = (rows) => { ... }
Purpose:

Formats and prints each row nicely like:

A | C | A
B | D | A
C | A | B
const getWinnings(rows, bet, lines) => { ... }
Logic:

Loops through each of the selected lines (top 1–3 rows).

If all symbols in a row are the same, the player wins:

A | A | A → Win!
Multiplies the bet by that symbol’s value (from SYMBOL_VALUES)
