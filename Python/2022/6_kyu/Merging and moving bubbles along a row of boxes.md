## Merging and moving bubbles along a row of boxes
###### `FUNDAMENTALS` `ALGORITHMS` `PUZZLES` `GAMES` `MATHEMATICS` `NUMBERS`

### Overview
Start with a row of empty boxes, and place `n` bubbles in the left-most box in the row. You may assume there are infinitely many boxes to the right.

At each step, you must pick any box with 2 or more bubbles currently inside it, ***merge 2 of the available bubbles in that box*** to form a new bubble (thereby reducing the total number of bubbles in the entire row by 1), then you must immediately ***move the new bubble rightwards*** into the ***immediate next neighbour*** box to the right.

You must continue doing this until you reach the final state in which you cannot merge any more bubbles; i.e. reach the state in which all boxes have ***at most one*** bubble in them.

For a given value of `n` initial bubbles placed in the left-most box in the row, ***what is the number of steps required to reach the final state?***

>Hint: In case you are wondering why we can ask for ***the*** number of steps, and the final state, regardless of how you choose your steps: the number of steps for a given value of `n` will always be the same no matter how you choose your steps - see the Walk-through Example below

### Inputs
You will be given an `integer`, `n`, representing the number of bubbles, which are all placed initially in the left-most box.

Performance requirement: You will be tested on values of `n` up to `200,000,000`.

### Outputs
Return an `integer`, representing the number of steps required to reach the final state.

### Walk-through Examples


```python
n = 10 bubbles

10 _ _ _ _
8 1 _ _ _
6 2 _ _ _ 
```

Note here that you can choose to either form `4 3 _ _ _` or `6 _ 1 _ _ _` let's pick the latter for this example:


```python
6 _ 1 _ _
4 1 1 _ _
2 2 1 _ _
```

Note here again that you can choose to either form `_ 3 1 _ _` or `2 _ 2 _ _` let's pick the former for this example:


```python
_ 3 1 _ _
_ 1 2 _ _
_ 1 _ 1 _ #final state
```

In this example we reached the valid final state - where all boxes contain at most one bubble - in `8` steps.

You can see in the above example that there may be more than one allowed move at any given step; for example, what if we had picked option `4 3 _ _ _` on the 2nd step?


```python
n = 10 bubbles, alternative choices

10 _ _ _ _
8 1 _ _ _
6 2 _ _ _
4 3 _ _ _ 
```

Here again there are multiple possible legal choices, let's pick one:



```python
2 4 _ _ _
```

Again, multiple possible legal choices, let's pick one:


```python
_ 5 _ _ _
_ 3 1 _ _
_ 1 2 _ _
_ 1 _ 1 _ #final state
```

Note how, with these alternative choices, we have reached the same final state as in previous example ***and in the exact same number of steps = 8*** as in previous example.

### My solution


```python
def moving_bubbles(n):
    if n == 1 or not n:
        return 0
    else:
        return (n // 2) + moving_bubbles(n // 2)
```

### Sample Tests


```python
from solution import moving_bubbles
import codewars_test as test

@test.describe("Fixed tests")
def tests():
    
    @test.it("Should obtain correct number of steps required to reach final state for n = 2, 10 initial bubbles")
    def test_n_small_numbers():
        test.assert_equals(moving_bubbles(2), 1, 'Returned number of steps required to reach final state for n = 2 initial bubbles is incorrect')
        test.assert_equals(moving_bubbles(10), 8, 'Returned number of steps required to reach final state for n = 10 initial bubbles is incorrect')
```
