layout: page
title: "Linked List"
permalink: /linked-list/

## Linked List

### 1. Reverse a linked list

* Iterate

```javascript
export class Solution {

  /**
   * reverse
   *
   * @param head: n
   * @return: The new head of reversed linked list.
   */
  reverse(head) {
        let p = head;
        let pre = null;
        while (p) {
            let nxt = p.next;
            p.next = pre;
            pre = p;
            p = nxt;
        }
        return pre;
  }
}
```

* Recursion

```javascript
export class Solution {

  /**
   * reverse
   *
   * @param head: n
   * @return: The new head of reversed linked list.
   */
  reverse(head) {
    if (!head || !head.next) return head;
    const tail = this.reverse(head.next);
    head.next.next = head;
    head.next = null;
    return tail;
  }
}
```

### 2. Reverse a linked list from position `m` to `n`

* 遍历一次 图解

![第一步](image/reverse-linked-list-II/1.png)

![第二步](image/reverse-linked-list-II/2.png)

![第三步](image/reverse-linked-list-II/3.png)

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} left
 * @param {number} right
 * @return {ListNode}
 */
var reverseBetween = function(head, left, right) {
    let dummy = new ListNode(null, head);
    let pre = dummy;
    for (let i = 1; i < left; i++) {
        pre = pre.next;
    }
    let cur = pre.next;
    for (let i = left; i < right; i++) {
        let nxt = cur.next;
        cur.next = nxt.next;
        nxt.next = pre.next;
        pre.next = nxt;
    }
    return dummy.next;
};
```

### 3. Reverse Nodes in k-Group

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var reverseKGroup = function(head, k) {

    const reverse = function(head) {
        let pre = null;
        while (head) {
            let nxt = head.next;
            head.next = pre;
            pre = head;
            head = nxt;
        }
        return pre;
    }

    let dummy = new ListNode(null, head);
    let pre = end = dummy;
    while (end) {
        for (let i = 0; i < k && end; i++) {
            end = end.next;
        }
        if (!end) break;
        let start = pre.next;
        let nxt = end.next;
        end.next = null;
        pre.next = reverse(start);
        start.next = nxt;
        pre = start;
        end = pre;
    }
    return dummy.next;
};
```
