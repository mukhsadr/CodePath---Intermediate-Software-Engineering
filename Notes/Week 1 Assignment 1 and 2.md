# Week 1 - Assignment 1 and 2

## [Assignment 1](#assignment-1)

* [Problem #1 - Reverse a String](#problem-1---reverse-a-string)

* [Problem #2 - Substring](#problem-2---substring)

* [Problem #3 - Next Prime](#problem-3-next-prime)

## [Assignment 2](#assignment-2-)

* [Problem #1 - Valid Palindrome](#problem-1---valid-palindrome)

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


### __Problem #3 - Next Prime__
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

## Assignment 2

### Problem #1 - Valid Palindrome

    A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

__Understand__

* Do we only consider the alphabet and numbers?
    * In this problem, we ignore all the characters except alphabets and numbers.
* What should function return if string is empty?
    * True

### Test case 1 - Happy case
    s = "Taco cat" ==> True
### Test case 2
    s = "race a car" ==> False
### Test case 3 - edge case
    s = " " ==> True

__Match__

* two pointers approach

__Plan__

* assign left pointer to 0 and right pointer to length of string minus 1
* look though each index from left to right and from right to left until they meet in the middle
* inside loop, check if char. in left pointer index is same with char in right pointer index:
    * if they do not match, return False, 
    otherwise, increment left pointer to 1 and decrement right pointer to 1 each time
* if loop finishes without returning False, return True
#### Check if string is alphanumeric
* check if char greater or equal to ASCII code of "A" or less or equal tASCII code of "Z"
* check if char greater or equal to ASCII code of "a" or less or equal tASCII code of "z"
* check if char greater or equal to ASCII code of "0" or less or equal tASCII code of "9"

__Implement__

```python
def validPalidrome(s:str) -> bool:

	left, right = 0, len(s)-1
	while left < right:
		while left < right and not isAlphaNum(s[left]):
			left += 1
		while right > left and not isAlphaNum(s[right]):
			right -= 1
		if s[left].lower() != s[right].lower():
			return False
		left, right = left+1, right-1
	return True

def isAlphaNum(s:str) -> bool:

	return (ord("A") <= ord(s) <= ord("Z") or
		ord("a") <= ord(s) <= ord("z") or
		ord("0") <= ord(s) <= ord("9"))

```

__Review__

* validPalidrome("Taco cat") ==> True
* validPalidrome("race a car") ==> False
* validPalidrome(" ") ==> True

__Evaluate__

* Space complexity - O(1)
* Time complexity - O(n)

### Problem #2 - Valid Palindrome II

    Given a string s, return true if the s can be palindrome after deleting at most one character from it.

__Understand__

* How do we verify if string is a palindrome of another string?
    * We compare str[i] and str[j], and iterate i++, j- -, we can verify it is palindrome because could not find str[i] != str[j].
* Can a string become a palindrome?
    * If str is not a palindrome, but if delete a character in string, it can become palindrome.

### Test case 1 - Happy case
    s = "aba" - return True
### Test case 2
    s = "abc" - return False
### Test case 3 - edge case
    s = "abca" - return True
    Explanation: You could delete the character 'c'.

__Match__

* two pointers approach 


__Plan__


* assign left pointer to 0 and right pointer to length of string minus 1
* loop through left to right index and right to left index until they meet
    * if left index in string doesn't match to right index:
        * assign skipLeft to s[left+1:right+1] where we skip current left pointer by incrementing 1
        * assign skipRight to s[left:right] where we skip current right pointer
    * check if skipLeft matches to reversed skipLeft by skipL == skipL[::-1]
    * check if skipLeft matches to reversed skipLeft by skipR == skipR[::-1]
    * increment left by 1 and decrement right by 1
* return True if loop finishes.

__Implement__
```python
def validPlandindrome2(s:str) -> bool:
	left, right = 0, len(s)-1
	while left < right:
		if s[left] != s[right]:
			skipL, skipR = s[left+1:right+1], s[left:right]
			return if skipL == skipL[::-1] or skipR == skipR[::-1]
		left, right = left+1, right-1
	return True

```

__Review__

* validPlandindrome2("aba") ==> True
* validPlandindrome2("abca") ==> True
* validPlandindrome2("abc") ==> False

__Evaluate__
* Space complexity - O(1)
* Time complexity - O(n)

### Problem #3 - Pow(x,n)
    Implement pow(x, n), which calculates x raised to the power n (i.e., xn).

__Understand__

- How do we stimulate the operation of evaluating exponents?
	An exponent can easily be evaluated by multiplying the base exponent number of times. So, we can easily simulate this using a loop.
- What if either exponent is equal to the maximum value of integer or minimum value of integer?
	When we have exponent as the minimum value of integer, the answer can be 
	either 1 or 0. If the base is 1 or -1, having exponent as integer’s minimum value, 
	will have answer as 1 otherwise 0. Similarly we can have only 1 with exponent as 
	maximum value of integer, because of the constraint on the output is below 10000.

Test case 1
x = 2.00000, n = 10 -  return 1024.00000
Test case 2
x = 2.10000, n = 3 - return 9.26100
Test case 3
x = 2.00000, n = -2 - return 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25

M-atch

	- recursive - We can implement fast modulo exponentiation either in a recursive 
			manner or iteratively. In fast modulo exponentiation, we multiply 
			the base in the power of 2. By this, we meant that we keep on multiplying 
			the base by itself. So, in the first step, the base becomes squared of itself.

P-lan

- Convert exponent in binary format and keep on multiplying the bases as per the exponent binary format.
- If we just use the normal way of calculation, when face 1 to the power of 10000, 
	the computation complexity is too high. Consider this way: if we want to get 2^10,
- Break into base case where n = 0 or n = 1 and recurrent relations where n is even or odd numbers.
- When n is odd, pow(x, n) = x * pow(x, n-1)
- When n is even, pow(x, n) = pow(x, n/2) * pow(x, n/2).
- Note when x is equal with 1.0, we could do a optimization here.
- Another corner case is when n is -2^31, -n will trigger a integer overflow.

I-mplement

def pow(x, n):
	def helper(x, n):
		if x == 0:
			return 0
		if n == 0:
			return 1
		result = helper(x*x, n//2)
		return x*result if n%2 else result
	result = helper(x, abs(n))
	return result if n>=0 else 1/result

R-eview

pow(2.00000, 10) - 1024.00000
pow(2.10000, 3) - 9.26100
pow(2.00000, -2) - 0.25000

E-valuate 
	
	-Space - O(1)
	-Time - O(logN) - because we used fast modulo exponentiation that takes logarithmic 
				time to compute the exponent over a base. We can also intuitively 
				find the time complexity. Since we have divided the exponent until 
				it became 0. Thus the time required is dependent on logN, where N 
				is the exponent.

Problem #4 Permutations

Given an array nums of distinct integers, return all the possible permutations. 
You can return the answer in any order.

U-nderstand

- What is a permutation?
	A permutation is nothing but an arrangement of given integers.
- What permutations are we returning in this problem?
	We return all possible arrangements of the given sequence.

Test case 1 - Happy case
nums = [1,2,3] - return [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
Test case 2 
nums = [0,1] - return [[0,1],[1,0]]
Test case 3 - edge case
nums = [1] - return [[1]]

M-atch
	
	Loop through the array, in each iteration, a new number is added to different 
	locations of results of previous iteration. Start from an empty List.

P-lan

 - The concept is to resolve the problem recursively by:
 - Pick one element in the list, and remove it from the list of available integers
 - Generate all the permutations for the remaining list and append them to the first element
 - To do that we keep track of current which is the currently available integers, 
	and permutation, which is the currently generated permutation.

I-mplement

def permute(nums):

    res = []
    n = len(nums)
    def solve(n, perm):
        if n==0:
            res.append(perm.copy())
            return None
        for i in range(len(nums)):
            if nums[i] in perm: continue
            perm.append(nums[i])
            solve(n-1, perm)
            perm.pop()
    solve(n, [])
    return res
permute([1,2,3])

R-eview

permute([1,2,3]) - return [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
permute([0,1]) - return [[0,1],[1,0]]
permute([1]) - return [[1]]

E-valuate

	Space - O(n!)
	Time - O(n*n)





