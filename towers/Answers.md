#  MCON 264 — Recursion Assignment: Towers of Hanoi × 3


##  Overview

In this lab, you implemented three recursive versions of the Towers of Hanoi problem and (optionally) one iterative version.  
Each part reinforces a key concept of recursion — base case, recursive case, and growth pattern — and illustrates how recursion can be refactored or replaced by iteration.

---

## Part 1 — Classic Towers of Hanoi (`TowersOfHanoi.java`)

### 1. Base Case
_Describe the base condition that stops recursion (for example, what happens when `n == 0`?)._

> ✎ Your answer here 
 if n == 0, stop. There are no disks to move.

### 2. Recursive Case
_Explain the sequence of recursive calls and what each represents._

> ✎ Your answer here
1.	Move n-1 disks from from → aux.
2.	Move the biggest disk from from → to.
3.	Move the n-1 disks from aux → to.
Each move is printed, total moves = 2^n - 1.

### 3. Sample Trace (for n = 3)

| Move # | From | To |
|:------:|:----:|:--:|
|   1    |  A   | C  |
|   2    |  A   | B  |
|   3    |  C   | B  |
|   4    |  A   | C  |
|   5    |  B   | A  |
|  6     | B    | C  |
|   7    |  A   | C  |

_Total moves = 2ⁿ − 1 = 7 (for n = 3)_

---

## Part 2 — Counting Moves (`TowersExercise21.java`)

### 1. Approach
_How did you modify the standard recursion to count rather than print moves?_

>  Your answer here
> I used the same recursive pattern but didn’t print anything.
Instead, I added a static int count variable and did count++ every time a move would happen.

### 2. Verification of Formula
_Complete the table and verify that count = 2ⁿ − 1._

| n | Expected (2ⁿ − 1) | Program Output | Matches? (Y/N) |
|:--:|:-----------------:|:--------------:|:--------------:|
| 1 |        1          |       1        |       Y        |
| 2 |         3         |       3        |       Y        |
| 3 |         7         |       7        |       Y        |
| 4 |        15         |       15       |       Y        |
| 5 |        31         |       31       |       Y        |

### 3. Reflection
_What changes when you replace printed moves with a counter? What are the pros and cons?_

> ✎ Your answer here
> The logic didn’t change, only what I did during each move.
Using a counter makes the recursion faster (no printing), but you don’t actually see the process happen.

---

## Part 3 — Hanoi Variation (`TowersVariations.java`)

### 1. New Rule
_Every move must pass through the middle peg. How does this alter the recursion?_

> ✎ Your answer here
> That means moving one disk from peg 1 to peg 3 actually takes two moves: 1 → 2, then 2 → 3.
The recursion has more steps to make sure that rule is always followed.

### 2. Observed Move Counts

| n | Expected ≈ 3ⁿ − 1 | Program Output | Matches? (Y/N) |
|:--:|:-----------------:|:--------------:|:--------------:|
| 1 |        2          |       2        |       Y        |
| 2 |         8         |       8        |       Y        |
| 3 |        26         |       26       |       Y        |
| 4 |        80         |       80       |       Y        |

### 3. Analysis
_Why does this variation grow faster than the standard version? How do additional move constraints affect complexity?_

> ✎ Your answer here
> This version grows faster because each move now happens in two hops instead of one.
So the number of moves triples with each extra disk instead of doubling.

---

## Comparative Analysis

### 1. Growth Patterns

| Version | Approx. Formula | Growth Type |
|:--|:--|:--|
| Standard | 2ⁿ − 1 | Exponential |
| Variation | 3ⁿ − 1 | Exponential (faster) |
| Iterative (Optional) | 2ⁿ − 1 | Same as recursive but loop based |

### 2. Stack Depth and Memory
_Estimate the maximum recursion depth before StackOverflowError and discuss how stack size (–Xss flag) affects this._

> ✎ Your answer here
> Each recursive call adds one frame to the call stack.
The depth equals n.
If n gets too large, the stack runs out of space and causes a StackOverflowError.
You can increase stack size with the -Xss flag, but the time will still explode exponentially.

---

## Part 4 — Beyond Recursion (Extra Credit)

### Iterative / Explicit-Stack Version (`TowersIterative.java`)

1. How does your iterative version simulate recursion?
2. How did you track pending calls or frames?
3. Which version (r vs iterative) is clearer? Why?

> ✎ Your answer here
> 1. It uses its own stack to keep track of what would normally be recursive calls,
     pushing and popping steps instead of calling methods.
> 2. Each stack item stored the disk count and peg info. I pushed sub-steps in
     reverse order so they ran in the right sequence when popped.
> 3. The recursive version is easier to read and understand, but the iterative one
     avoids stack overflow and shows how recursion actually works behind the scenes.


---

## Discussion &amp; Reflection

1. What three questions can you use to verify a recursive solution works?
2. How do the base case and recursive case cooperate to guarantee termination?
3. What is the trade-off between elegance and efficiency in recursion?

> ✎ Your answers here
> 1. What’s the base case?
     How does the recursive case get smaller?
     Does it eventually reach the base case?
> 2. The base case stops it. The recursive case breaks the problem down until it reaches that stop.
> 3. Recursive code looks cleaner and easier to read, but it’s slower and uses more memory than a loop for large n.


---

## References (APA or MLA format)

- Dale, N., Joyce, D., &amp; Weems, C. (2016). *Object-Oriented Data Structures Using Java* (Ch. 3 Recursion). Jones &amp; Bartlett.
- Additional videos or websites you consulted (YouTube CS50 Recursion, GeeksForGeeks Hanoi, etc.)

---

 **Submission Checklist**

- [ ] `TowersOfHanoi.java` — implemented and tested
- [ ] `TowersExercise21.java` — counts moves correctly
- [ ] `TowersVariations.java` — middle-peg constraint implemented
- [ ] (Extra Credit) `TowersIterative.java` — loop or explicit stack solution
- [ ] All JUnit tests pass (green on GitHub Actions)
- [ ] This `ANSWERS.md` file completed and committed to repo  
