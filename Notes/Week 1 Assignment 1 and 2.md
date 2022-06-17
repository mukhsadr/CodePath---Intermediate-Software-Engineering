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

__Match__

* Two pointer approach (left and right pointer variables)

__Plan__

* check if substring is empty, if so return True (Edge case)
* assign two pointers to 0: one is for string and the other one is for substring.
* loop though each char of string:
    * check if char at index of string matches to char of substring:
        * if they match, increment pointer of substring by 1 to check the rest of chars in substring
		and check if the pointer is equal to its length: if so, return True (So, we know that every chars of substring is found in string)
* return False, after loop finishes (by this, I meant substring does not match to string and return False).

__Implement__
```python
def isSubStringTwoPointer(string:str, substring:str):
    if len(substring) == 0:
        return True
    stringPointer, subStringPointer = 0, 0
    while stringPointer < len(string):
        if string[stringPointer] == substring[subStringPointer]:
            subStringPointer += 1
            if subStringPointer == len(substring):
                return True
        stringPointer += 1
    return False
```

__Review__

* isSubStringTwoPointer("laboratory", "rat") ==> True
* isSubStringTwoPointer("cat", "meow") ==> False

__Evaluate__
	
* Space complexity - O(1)
* Time complexity - O(n*m)


### __Problem #3: Next Prime__
 Given a number, return the next smallest prime number Note: A prime number is greater than one and has no other factors other than 1 and itself.

__Understand__

* Is there guaranteed to be a solution?
    * Yes!
* Is the input number guaranteed to be positive?
    * No! This will cause edge case catching important!
* What makes a number prime? What does this number have to satisfy
    * HINT: A prime number only has factors of itself and 1.
    * This means 2, 3, 4, 5 … N-1 are not factors of this number

### Test case 1 - happy case
	input: 5 ==> 7
### Test case 2
	input: 1 ==> 2
### Test case 3 - edge case
	input: -10 ==> 2 (The smallest prime number is 2, so any input less than 2 should return 2)

__Match__

This problem may be hard to match to a specific problem pattern since it relies on general math intuition.

__Plan__

* before checking the number, increment it by 1 so it won't return number itself if it is already prime.
* start with base case where input is prime or not, if it is prime, return the number
* DO NOT FORGET that we have edge cases where if the input is negative, return 2
* otherwise, call the recursive function and increment the number by 1 until it returns True if it is next prime
* in base case, we call another isPrime function to check the number by which we increment by 1 in recursive function
* isPrime function check if the number is prime, if so, it returns True, otherwise, return False, which in turn revokes recursive function.

__Implement__

```python
def nextPrime(n):
    n += 1
    if isPrime(n):
        if n <= 1:
            return 2
        return n
    return nextPrime(n)
def isPrime(n, div = None):
    if div is None:
        div = n - 1
    while div >= 2:
        if n % div == 0:
            return False
        else:
            return isPrime(n, div-1)
    else:
        return True
```

__Review__

* nextPrime(5) ==> 7
* nextPrime(1) ==> 2
* nextPrime(-10) ==> 2

__Evaluate__

* Space complexity - O(1)
* Time complexity - O(n)? (not sure yet)
	





