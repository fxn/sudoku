This is a fairly simple Sudoku solver written in C. An exercise in bactracking I did back in 2005 to cheat in a contest of a newspaper. They published a daily Sudoku, and you had to send the solution to win something I have forgotten. Come on, who wants to solve a Sudoku when you can solve them all, uh?

The backtracking loop is compact, it is kind of generic to many backtracking problems I believe.

There is a matrix that stores the numbers, and there are redundant structures for rows, columns, and the nine sub-squares that maintain bit masks. They allow the program to check stuff using bitwise operators, which proved to be a fast approach compared to other options.

Other than that, the program is not very smart, just brute force backtracking with the obvious optimizations.

To compile _sudoku.c_ run

    gcc -O3 -std=c99 -o sudoku sudoku.c

The program receives the square as a series of numbers of three digits. Each argument represents one of the known numbers in the Sudoku and is entered as _row-col-number_, where _row_ and _col_ are 1-based.

This is for example the solution to the [Sudoku in the Wikipedia](http://en.wikipedia.org/wiki/Sudoku):

    $ time ./sudoku 115 123 157 216 241 259 265 329 338 386 418 456 493 514 548 563 591 617 652 696 726 772 788 844 851 869 895 958 987 999
    +---------+---------+---------+
    | 5  3  4 | 6  7  8 | 9  1  2 |
    | 6  7  2 | 1  9  5 | 3  4  8 |
    | 1  9  8 | 3  4  2 | 5  6  7 |
    +---------+---------+---------+
    | 8  5  9 | 7  6  1 | 4  2  3 |
    | 4  2  6 | 8  5  3 | 7  9  1 |
    | 7  1  3 | 9  2  4 | 8  5  6 |
    +---------+---------+---------+
    | 9  6  1 | 5  3  7 | 2  8  4 |
    | 2  8  7 | 4  1  9 | 6  3  5 |
    | 3  4  5 | 2  8  6 | 1  7  9 |
    +---------+---------+---------+

    real	0m0.003s
    user	0m0.001s
    sys		0m0.002s

This is the puzzle that a Finnish mathematician [claims to be the hardest one known for a human](http://www.efamol.com/efamol-news/news-item.php?id=43):

    $ time ./sudoku 118 233 246 327 359 372 425 467 554 565 577 641 683 731 786 798 838 845 881 929 974
    +---------+---------+---------+
    | 8  1  2 | 7  5  3 | 6  4  9 |
    | 9  4  3 | 6  8  2 | 1  7  5 |
    | 6  7  5 | 4  9  1 | 2  8  3 |
    +---------+---------+---------+
    | 1  5  4 | 2  3  7 | 8  9  6 |
    | 3  6  9 | 8  4  5 | 7  2  1 |
    | 2  8  7 | 1  6  9 | 5  3  4 |
    +---------+---------+---------+
    | 5  2  1 | 9  7  4 | 3  6  8 |
    | 4  3  8 | 5  2  6 | 9  1  7 |
    | 7  9  6 | 3  1  8 | 4  5  2 |
    +---------+---------+---------+

    real    0m0.006s
    user    0m0.004s
    sys     0m0.001s

The exact milliseconds vary a little between runs, but those are the magnitudes. Those examples ran in my MacBook Air 11'' mid-2012, with a dual core i7 (Ivy Bridge).

Since this was an exercise control error of the arguments is totally primitive. Basically, you either enter the right stuff or else get a segmentation fault.
