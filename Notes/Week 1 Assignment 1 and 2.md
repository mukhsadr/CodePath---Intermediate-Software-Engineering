# Week 1 - Assignment 1 and 2

## [Assignment 1](#assignment-1)

* [Problem #1 - Reverse a String](#problem-1---reverse-a-string)
* [Problem #2 - Substring](#problem-2---substring)
---

### __Problem #1 - Reverse a String__

Write a function that reverses a string.

__Understand__

* Can elements of the string be both characters and numbers?
    * Yes
* Can string be empty?
    * Yes
* Is there any time and space complexity?
    * Do not worry about them now.

### Test case 1 - Happy case
Input: "REVERSE" ==> "ESREVER" 
### Test case 2
Input: "42 Wallaby Way, Sydney" ==> "yendyS ,yaW yballaW 24"
### Test case 3 - Edge case
Input: ""  ==>  ""

__Match__

* Two pointer approach (left and right pointer variables)
* Recursion approach

__Plan__

* create array of string's characters
* assign left pointer to 0 and right pointer to length of string minus 1.
* loop though each element of array and check left pointer is less than right pointer so that they meet in the middle.
    * swap left pointer element with right pointer element
    * increment left pointer by 1 and decrement right pointer by 1
* return reversed string

__Implement__
```python
def reverseString(string:str) -> str:
    array = list(string)
    left, right = 0, len(string)-1
    while left < right:
        array[left], array[right] = array[right], array[right]
        left, right = left+1, right-1
    return "".join(array)
```

__Review__

* reverseString("REVERSE") ==> "ESREVER" 
* reverseString("42 Wallaby Way, Sydney") ==> "yendyS ,yaW yballaW 24"
* reverseString("") ==> ""

__Evaluate__

* Time complexity - O(n)
* Space complexity - O(n)

### __Problem #2 - Substring__
Write a function that takes in two strings and returns true if the second string is substring of the first, and false otherwise.

__Understand__

* Are both inputs string?
    * yes, now worries now
* what is returned?
    * Boolean, if the second string is substring of the first, true. Otherwise, false
* Can second input's length be longer than first input?
    * No, no worries now

### Test case 1 - Happy case
Input: "CATDOG", "ATDO" ==> True
### Test case 2
Input: "CATDOG", "ATDOGE"  ==> False
### Test case 3 - Edge case
Input: "CATDOG", ""  ==> True

