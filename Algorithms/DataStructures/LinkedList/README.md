# LinkedList Problems


## Easy Problems


### 1. Delete Ndoe in a Linked List

Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.
The assumptions are

1. There are at least 2 nodes
2. The selected node is not the tail node
3. All node values are unique

Because we don't know the previous node, we can't modify the previous node pointer. Initially I thought you had to loop through the whole linked list and replace the value for each one to shift the linked list.

```javascript
const deleteNode = (node) => {
    current = node;
    while (current.next !== null) {
        current.val = current.next.val;
        current = current.next
    }
}
```

However all you need to do is replace the value of the removed node with the next and have its pointer point to the next node's next pointer. *Mindblown*

```javascript
const deleteNode = (node) => {
    node = node.next.val;
    node.next = node.next.next;
};
```

### 2. Reverse Linked List

Reverse a singly linked list.

#### Example

```
Input: 1->2->3->4->5->NULL

Output: 5->4->3->2->1->NULL
```

Assumptions is that the linked list may be empty. The pointer to the NULL should only be from the Tail node.

Edge case: Either if the linked list is empty or there is only one node.

Iterative method: Keep track of your prev. node, current node and your current node's next pointer. You need your previous node to set it to your current next pointer and your current next to iterate through the linked list.

```javascript
const reverseList = (head) => {
    let current = head;
    let prev = null;
    let next = null;
    
    while (current !== null) {
        next = current.next;
        current.next = prev;
        prev = current;
        current = next;
    }
    return prev;
};
```

Recursive method:
