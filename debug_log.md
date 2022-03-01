# Debug Log

**Explain how you used the VSCode debugger tools to uncover the bugs in Exercise 7. Be specific. What breakpoints did you set? Where did you step to? What made you realize the error?**

_Example: I set a breakpoint on line 5 and stepped until line 12. There, I discovered that the `x` variable had a value of `-3`, whereas it should have had a value of `7`. That made me realize that we should be adding the two numbers `x` and `y`, instead of subtracting._

## Exercise 5

I ran the code and got a `list index out of range` error. I set a breakpoint on line 18 to step through the bubble sort algorithm. Whenever the code got to line 13 to call the `swap` function, I stepped over it because I know the problem is in the `bubble_sort`.

I watched the `i` variable increase until `5` was assigned to it by the for loop controls. This is problematic because of the line that makes the following comparison: `if list_of_nums[i] > list_of_nums[i+1]:`

Since `[i+1]` is being used, we need to ensure that the for loop declaration is set up in a way that an index error won't be thrown.

The problem can be solved by changing the for loop declaration on line 11 from `for i in range(len(list_of_nums)):` to  `for i in range(len(list_of_nums) - 1):`

## Exercise 7

### Bug 1

The expected output is `'fantastic, I guess programming is fantastic.'` but the actual output is `'fantastic'`.

To solve the problem, I started by setting a breakpoint on line 18 and stepped into each line of the code. I watched the variables change to see what's going on. On line 10, the variable `remainder_of_sentence` was declared, but its value was assigned as an empty string: `''`. I analyzed the line and noticed that the variable was being assigned by taking a slice of `start_str` as follows: `start_str[len(start_str):]`.

This is causing the problem. It can be resolved by updating the line to properly use the entire string instead of just the subsection that we want to replace. Corrected code: `sentence[len(start_str):]`

### Bug 2

I reran the code and this time the output was `'fantastic,kay'`. This is a bit better, but there's still a problem.

I kept my breakpoint on line 18 and stepped through the code again while watching the variables change.

When the recursive case was called on line 13, the `sentence` variable in the following call stack instance was set to `'kay'` rather than the remainder of the entire sentence. This is a similar issue to the first bug, and the solution should be similar as well.

On line 13, I updated the recursive call from `return sentence[0] + replace_substring(start_str[1:], start_str, replace_str)` to `return sentence[0] + replace_substring(sentence[1:], start_str, replace_str)` and that resolved the problem.
