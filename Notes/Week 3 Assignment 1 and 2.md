# Week 3 - Assignment 1

## [Assignment 1](#assignment-1)

* [Problem #1 - Remove Duplicates from Sorted List](#problem-1---remove-duplicates-from-sorted-list)

* [Problem #2 - Linked List Cycle](#problem-2---linked-list-cycle)

* [Problem #3 - Merge Two Sorted Lists](#problem-3---merge-two-sorted-lists)

* [Problem #4 - Remove Duplicates II](#problem-4---remove-duplicates-ii)

---

### Problem #1 - Remove Duplicates from Sorted List

__Understand__

    Given a sorted linked list, delete all duplicates such that each element appear only once.

* Is that guaranteed elements are sorted?
    * Yes
* Is that guaranteed the list has duplicates?
    * No
* What should the function return?
    * head with each element appears only once.
* Can elements be all integers, negative or any invalid input?
    * length can be between 0 to 100, all positive integers.
* Is there any time or space complexity?
    * No worries now.

### Test case 1 - Happy case
    input: [1->2->3->3>4] ==> [1->2->3->4]
### Test case 2
    input: [1->2->3->4] ==> [1->2->3->4]
### Test case 3 - Edge case
    input: [] ==> []

__Match__

* Two pointer approach

__Plan__
* assign current pointer to head
* loop through each element and assign current to current.next:
    * in the loop, create another loop to check if current element's value and current element's next value are equal:
            * if so, assign current element's next to current next next
    * update current to current next
* return head
__Implement__

```python
def deleteDuplicates(head):
    current = head
    while current:
        while current.next and current.next.val == current.val:
            current.next = current.next.next
        current = current.next
    return head
```

__Review__

__Evaluate__
* Time complexity O(n)
* Space complexity O(1)

### Problem #2 - Linked List Cycle

    Given a linked list, determine if it has a cycle in it. For simplicity, assume the linked list cannot have more than 1000 nodes in it.

__Understand__

* Is that guaranteed that list has a cycle?
    * No
* What should the function return?
    * Boolean: true if it has a cycle, otherwise false
* Can the list be empty?
    Yes, length can be between 0 to 100
* Is there any time or space complexity?
    * no worries now

### Test case 1 - Happy case
    input: [1->2=>3->4->5=>] k => 3 ==> True
### Test case 2
    input: [1->2->3->4->5] k => None ==> False
### Test case 3 - Edge case
    input: [] ==> False

__Match__

* Two pointer approach (slow and fast pointers)

__Plan__

* assign slow and fast pointers to head
* check fast and fast next elements are not None
    * loop though in this condition:
        * increment slow pointer by one node and fast pointer by two nodes at a time
        * check if slow and fast pointers are equal, if so return True
    * return False if loop ends without returning True

__Implement__

```python
def hasCycle(head):
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```

__Review__

__Evaluate__

* Time complexity O(n)
* Space complexity O(1)

### Problem #3 - Merge Two Sorted Lists

    Merge two sorted linked lists.

__Understand__

* Is that guaranteed elements are sorted?
    * Yes
* Can either input be empty?
    * Yes
* Can length of inputs not be equal?
    * Yes, append leftover to the tail if either of input has more nodes
* Can the node values be negative?
    * Yes. The node values will fall between -100 and 100.
* Can we create new nodes?
    * No. The question asks you to splice the given nodes.
* Is there any time or space complexity?
    * no worries now but can you solve it with constant space

### Test case - Happy case
    input: [1->2->3], [2->4] ==> [1->2->2->3->4]
### Test case - Edge case
    input: [1->2->3], [] ==> [1->2->3]

__Match__

* Two pointer approach (tail)
* Dummy head

__Plan__

* create dummy head from a new List Node
* assign tail to dummy head so we can add elements from list1 and list2
* in while loop, check list1 and list2 are not None:
    * if list1' element val is less than list2's element val:
        * assign list1 to tail next
        * increment list1 by one node
    * else: 
        * assign list2 to tail next
        * increment list2 by one node
    * assign tail to tail next so it moves forward till either list1 or list2 reaches its end and return None in while loop.
* after loop ends and if there is any leftover in either list1 or list2, check list1 in not None:
    * assign leftover list1 elements to tail next
* else if list2 has leftover elements:
    assign leftover list2 elements to tail next
* return dummy next

__Implement__
```python
class ListNode:
     def __init__(self, val=0, next=None):
         self.val = val
         self.next = next

def mergeTwoLists(list1, list2):
    dummy = ListNode()
    tail = dummy
    while list1 and list2:
        if list1.val < list2.val:
            tail.next = list1
            list1 = list1.next
        else:
            tail.next = list2
            list2 = list2.next
        tail = tail.next
    if list1:
        tail.next = list1
    elif list2:
        tail.next = list2
        
    return dummy.next
        
```

__Review__

__Evaluate__

* time complexity O(n*m) not sure because we loop through till n and still have to deal with leftover. Is assigning leftover to tail next constant time?
* space complexity O(n*m)not sure because we loop through till n and still have to deal with leftover. Is assigning leftover to tail next constant space?

### Problem #4 - Remove Duplicates II

    Given a linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Can you do it without taking up extra memory?

__Understand__
* Is that guaranteed the list has duplicates?
    No
* What should the function return?
    * linked list with distinct numbers
* What are nodes values? Integer, string, positive or negative numbers?
    * -100 <= Node.val <= 100
* Is the list sorted?
    * Yes, the list is guaranteed to be sorted in ascending order.
* Is there any time or space complexity?
    * Yes, can you do it without taking up extra memory?
* Can the input list be empty?
    * No. Assume the input list will have anywhere from 1 node to 30000 nodes.
### Test case 1 - happy case
    input: 1->2->3->3->4->4->5  ==> 1->2->5 
### Test case 2
    Input: 1->1->1->2->3  ==> 2->3
### Test case 3 - Edge case
    Input: 5->6->3->5  ==> 6->3 or 3->6

__Match__

* dummy head approach
* two pointer approach (prev and current)

__Plan__

* create a dummy head from a new List Node (0, head)
* assign prev pointer to dummy head
* loop though each node till it reaches its end:
    * check current next is not None and current node's value is equal to next node's value:
        * if so, loop though to skip and assign current node to next node
        * update prev node to current next node
    * else: update prev node to prev next node
    * update current node to current next node
* return dummy next

__Implement__

```python
class ListNode:
     def __init__(self, val=0, next=None):
         self.val = val
         self.next = next

def deleteDuplicates(head):
        dummy = ListNode(0, head)
        prev = dummy
        while head is not None:
            if head.next is not None and head.val == head.next.val:
                while head.next is not None and head.val == head.next.val:
                    head= head.next
                prev.next = head.next
            else:
                prev = prev.next
            head = head.next
        return dummy.next
```

__Review__

__Evaluate__

* time complexity O(n)
* space complexity O(1)