Download Link: https://assignmentchef.com/product/solved-cs1010-assignment-7
<br>
# Question 1: Walk—————————–

Many cities in the world, such as New York City, are laidout as a grid, with streets running in the north-southdirections and east-west directions.  Buildings between twostreets are called _blocks_.

Suppose we start at a junction of two streets, and we wishto walk to another junction that is $y$ blocks to the northand $x$ blocks to the east, how many possible paths arethere to walk to the destination?

For example, suppose we want to walk to a junction that isone block to the north and one block to the east, and we canonly walk eastward and northward, there are two possiblepaths.  We can walk east for one block, then walk north foranother block.  Or, we can walk north first for one block,then walk east for another block.

The figure below illustrates the scenario, where we arepositioned at source D and we wish to go to destination B.The two possible paths are DAB and DEB.

“`A—B—C|   |   |D—E—F“`

Suppose now we want to walk to C, a junction that is twoblocks to the east, and one block to the north.  There arethree different possible paths.  The three paths are DABC,DEBC, DEFC.

Write a program `walk` that reads in two integers x and y (x&gt;= 0, y &gt;= 0), and prints the number of possible paths wecan walk to the destination that is x block to the east andy block to the north.

### Grading Criteria

The grading criteria for this question is:

|              | Marks ||————–|——-|| Correctness  | 5     || Efficiency   | 5     |

Your solution must take no more than O(xy) time to obtainthe full efficiency marks.

Hint: Think recursively, but solve iteratively.

## Sample Run————-“`<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="1a7575736d6e5a6a7f2b2b2b">[email protected]</a>:~/as08-ooiwt$ walk10 01<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="503f3f392724102035616161">[email protected]</a>:~/as08-ooiwt$ walk1 12<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="137c7c7a6467536376222222">[email protected]</a>:~/as08-ooiwt$ walk2 26“`

# Question 2: Maze—————————–

Agent Scully woke up and found herself in the dark.  Shefigured out that she is in a maze.  She has to find her wayout if there is one!

The maze can be simplified as a grid of (m x n) cells. Eachcell can be of the following:

1. ‘#’ denotes a segment of a wall.  No one can pass throughthe walls.

2. ‘.’ denotes an empty space

3. ‘@’ denotes where Scully is at currently. It is also anempty space

Anytime Scully reaches a border cell (a cell in either thetop-most or bottom-most row or left-most or right-mostcolumn), she escapes the maze and can go save her partnerAgent Mulder.  She can only move from one empty space toanother adjacent cell in one step.  Two cells are adjacentif they share a common edge.

Scully took CS1010, and she got a concrete plan to seek away out by trial and error.  She follows **strictly** thefollowing strategy to find a way through the maze startingfrom her initial position.  At each time step,

1. She looks for an empty adjacent cell that has never beenvisited yet, in the sequence of up/right/down/left to thecurrent cell she is at.  If there is an empty adjacent cell,she moves to that cell.  The cell she moves to is nowvisited.

2. If no empty, unvisited, adjacent cell exists, shebacktracks on the path that she comes from, moving one stepback, and repeat 1 again.

In this way, Scully will systematically explore the maze,with no repetitive visit of any cell more than once exceptwhen she backtracks.  She will stop when successfullyescaped the maze, or finds that there is no way out afterbacktracking all the way back to the original position.  Sheis completely trapped within the maze and now must wait forAgent Mulder to come and free her.

Write a program `maze.c`, that reads from standard input.First, read two positive integers m and n, followed by mlines of n characters in each line that represents the mazesetup.  One and only one `@` will be present in the mazesetup.

The program then prints, to standard output, an animation of$k$ iterations. The output should only contain $m$ rows with$n$ characters in each row, with an additional row at last.Similarly, you must use `#` to represent a wall, a `.` torepresents empty space, and `@` to represent where Scully isat.  After printing the maze, your program prints the numberof steps that Scully has made.

You should use recursion to explore the maze and look for away out.

Here is an example.  The following is the starting positionof Scully and the maze.

“`############.#…..#.##.#####.#.##.#…#.#.##.#.#…..##.#.##.#.###@#.#..#..##…#.#.#..###########0“`

Scully firstly moves five steps up:“`############@#…..#.##.#####.#.##.#…#.#.##.#.#…..##.#.##.#.###.#.#..#..##…#.#.#..###########5“`

At this point, Scully is stuck since there is no moreadjacent empty cell that has not been visited.  Scully thenbacktracks:“`############.#…..#.##.#####.#.##.#…#.#.##.#.#…..##.#.##.#.###@#.#..#..##…#.#.#..###########10“`

Scully then moves down:“`############.#…..#.##.#####.#.##.#…#.#.##.#.#…..##.#.##.#.###.#.#..#..##@..#.#.#..###########11“`

Then right:“`############.#…..#.##.#####.#.##.#…#.#.##.#.#…..##.#.##.#.###.#.#..#..##<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="8aa4a4ca">[email protected]</a>#.#.#..###########13“`

Then up:“`############.#…..#.##.#####.#.##.#@..#.#.##.#.#…..##.#.##.#.###.#.#..#..##…#.#.#..###########17“`

Then right (two steps) and then down (two steps) and thenright (two steps):

“`############.#…..#.##.#####.#.##.#…#.#.##.#.#<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="ebc5c5abc5c5">[email protected]</a>##.#.##.#.###.#.#..#..##…#.#.#..###########22“`

Then Scully moves up and left, and she is stuck again.

“`############.#@….#.##.#####.#.##.#…#.#.##.#.#…..##.#.##.#.###.#.#..#..##…#.#.#..###########29“`

At this point she backtracks:

“`############.#…..#.##.#####.#.##.#…#.#.##.#.#<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="6b45452b4545">[email protected]</a>##.#.##.#.###.#.#..#..##…#.#.#..###########36“`

Moves right, and up, and stuck again!

“`############.#…..#@##.#####.#.##.#…#.#.##.#.#…..##.#.##.#.###.#.#..#..##…#.#.#..###########41“`She backtracks again,

“`############.#…..#.##.#####.#.##.#…#.#.##.#.#…@.##.#.##.#.###.#.#..#..##…#.#.#..###########45“`

This time she found her way out!

“`############.#…..#.##.#####.#.##.#…#.#.##.#.#…..##.#.##.#.###.#.#..#..##…#.#.#<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="567816">[email protected]</a>###########50“`

It took her a total of 50 steps to exit the maze.