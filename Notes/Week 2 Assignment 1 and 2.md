# Week 2 - Assignment 1 and 2

## [Assignment 1](#assignment-1)

* [Problem 1 - Element with a frequency of K](#problem-1---element-with-a-frequency-of-k)

* [Problem 2 - Longest Consecutive Subsequence](#problem-2---longest-consecutive-subsequence)

## [Assignment 2](#assignment-2)

* [Problem 1 - Majority Element](#problem-1---majority-element)

* [Problem 2 - Roman to Integer](#problem-2---roman-to-integer)


---

### Problem 1 - Element with a frequency of K

    Find the element that appears k number of times in an array.



__Understand__

* Are there any time and space complexities?
    * No,
* What should the function return?
    * the element that appears k number of times
* What should the function return if there is no element that appears K times?
    * None
* Can the input be empty?
    * Yes. return None

### Test case 1 - Happy case
    input: [8, 7, 9, 6, 7, 5, 1], k = 2  ==> 7
### Test case 2
    input: [0, 1, 2, 3, 4] k = 2   ==> None
### Test case 3 - Edge case
    input: [0, 0, 1, 1] k = 2  ==> 0 or 1
### Test case 4 - Edge case
    input: [] k = 4  ==> None

__Match__

* Hash Map

__Plan__
* if length of input is 0, return None
* create a hash map to store elements of list as key and occurrence as value
* loop though each element and store it in hash map as key:
    * if element was stored in hash map already, increment its value by 1
    * check if value is equal or greater than k, return the key
    * if it was seen before, store it in hash map

* hashMap = {8:1, 7:2, 9:1, 6:1, 5:1} k=2 ==> 7
* hashMap = {0:1, 1:1, 2:1, 3:1, 4:1} k=2  ==> None
* hashMap = {0:2, 1:2} k=2 ==> 0 or 1
* hashMap = {} k=4  ==>None

__Implement__

```python
def frequencyOfK(array, k):
    if len(array) == 0:
        return None
    hashMap = {}
    for i in range(len(array)):
        if array[i] in hashMap:
            hashMap[array[i]] += 1
            if hashMap[array[i]] >= k:
                return array[i]
        else:
            hashMap[array[i]] = 1
```

__Review__
* frequencyOfK([8, 7, 9, 6, 7, 5, 1], 2) ==> 7
* frequencyOfK([0, 1, 2, 3, 4], 2) ==> None
* frequencyOfK([0, 0, 1, 1], 2) ==> 0 or 1
* frequencyOfK([], 4) ==> None

__Evaluate__

* Time complexity - O(n)
* Space complexity - O(n)


### Problem 2 - Longest Consecutive Subsequence

    Given an unsorted array of integers, we want to find the length of the longest subsequence such that elements in the subsequence are consecutive integers. The consecutive numbers can be in any order.

__Understand__

* Is the input always positive integers?
    * No, -109 <= nums[i] <= 109
* Can list be empty?
    * Yes, 0 <= nums.length <= 105 and return 0
* Is that guaranteed the list has consecutive numbers
    * yes
* Is there any time or space complexity?
    * Can you solve it with O(n)
### Test case 1 - Happy case
    Input: [1, 9, 3, 10, 4, 20 , 2] ==> 4
### Test case 2 - Edge case
    input: [] ==> 0
### Test case 2 - Edge case
    input: [2] ==> 1

__Match__

* Hash Set - to store unique values
* Book keeping approach - to store longest consecutive numbers

__Plan__

* create hashSet and store elements of list
* create variable to store longest consecutive numbers and set it to 0
* loop through each element in list:
    * if current element minus 1 is not in hashSet:
        * create a variable to store length of current consecutive numbers and set length to 0
        * loop though rest by adding length to current element and check if it is in hashSet, if so, increment length by 1 at a time
        * reassign longestCon by comparing max of either length or longestCon
* return longestCon

__Implement__
```python
def longestConsecutiveSubsequence(array):
    hashSet = set(array)
    longestCon = 0
    for num in array:
        if num-1 not in hashSet:
            length = 0
            while num+length in hashSet:
                length += 1
            longestCon = max(longestCon, length)
    return longestCon

```
__Review__

* longestConsecutiveSubsequence([1, 9, 3, 10, 4, 20 , 2]) ==> 4
* longestConsecutiveSubsequence([]) ==> 0
* longestConsecutiveSubsequence([2]) ==> 1

__Evaluate__

* time complexity - O(n)
* space complexity - O(n)

## Assignment 2

### Problem 1 - Majority Element

    Given an array nums of size n, return the majority element.
    The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

___Understand__

* What should the function return if input is empty?
    * None
* Is there any time or space complexity?
    * No
* What should function return if input has equal amount of majority number? [2,2,1,1]
    * You may assume that the majority element always exists in the array. So [2,2,1,1] is invalid input

### Test case 1 - Happy case
    input: [1,1,1,2]  ==> 1
### Test case 2 - Edge case
    input [2,2,1,1] ==> None because it is invalid input


__Match__

* Hash Map


__Plan__

* create a hash map to store numbers as key and count as value
* create a variable to store half length of list
* loop though each element and store it in hash map
    * if key already exists, increment value by 1
    * check value is greater than majority elements in the list 
        * if so return the key
    if it doesn't exit, add key to hash map and set its value to 1


__Implement__

```
def majorityElement(array):
    dict = {}
    floor = len(array) // 2
    for i in range(len(array)):
        if array[i] in dict:
            dict[array[i]] += 1
            if dict[array[i]] > floor:
                return array[i]
        else:
            dict[array[i]] = 1
```

__Review__

* majorityElement([1,1,1,2]) ==> 1

__Evaluate__

* time complexity - O(n)
* space complexity - O(n)

### Problem 2 - Roman to Integer
    Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.
    For example, 2 is written as II in Roman numeral, just two ones added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

    Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

    I can be placed before V (5) and X (10) to make 4 and 9. 
    X can be placed before L (50) and C (100) to make 40 and 90. 
    C can be placed before D (500) and M (1000) to make 400 and 900.

___Understand__

* Is it easier to iterate from right to left or left to right?
    * Subtractive numerals is that they appear before a larger number, which means they are easier to identify if we iterate from right to left than left to right.
* How can a dictionary help here?
    * A dictionary can map the basic roman numeral to its appropriate values

### Test case 1
    Input: s = "III"  ==> 3
    Explanation: III = 3.
### Test case 2
    Input: s = "LVIII" ==> 58
    Explanation: L = 50, V= 5, III = 3.

### Test case 3
    Input: s = "MCMXCIV" ==> 1994
    Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.


__Match__

* Hash Map

__Plan__

* Create a hash map and store roman numbers
* create variable to store total amount and set it to 0
* loop though each char in string:
    * check if string index is not out of range
    * check current char is smaller than next char by checking hashMap, if so, minus value from total
    * if current char' value is bigger than next char value, add value to total
* return total value


__Implement__

```python 
def romanToInteger(s):
    dict = {'I':1, 'V':5, 'X':10, 'L':50, 'C':100, 'D':500, 'M':1000}
    total = 0
    for i in range(len(s)):
        if i+1 < len(s) and dict[s[i]]<dict[s[i+1]]:
            total -= dict[s[i]]
        else:
            total += dict[s[i]]
    return total
```

__Review__
* romanToInteger("III") ==> 3
* romanToInteger("LVIII") ==> 58
* romanToInteger("MCMXCIV") ==> 1994


__Evaluate__

* time complexity - O(n)
* space complexity - O(1)

