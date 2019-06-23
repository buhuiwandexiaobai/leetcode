#### 题目：两个非空链表，表示两个非负整数。 数字以相反的顺序存储，每个节点包含一个数字。 两个计算两个数字的和并将其作为链接列表返回。您可以假设这两个数字不包含任何前导零，除了数字0本身。
例如 Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.

#### 思路：因为数字是以相反的方向存储的，所以我们可以直接从两个链表的头部开始相加。思想与合并两个有序链表相似。

代码：
```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    var p = l1,
        q = l2,
        jin = 0,
        rHead = new ListNode(-1),
        rear = rHead;
    ;
    while(p !== null && q !== null) {
        let newNode = new ListNode((p.val + q.val + jin) % 10);
        jin = Math.floor((p.val + q.val + jin) / 10);
        rear.next = newNode;
        rear = newNode;
        p = p.next;
        q = q.next;
    }
    while( p !== null) {
        let newNode = new ListNode((p.val + jin) % 10);
        jin = Math.floor((p.val + jin) / 10);
        rear.next = newNode;
        rear = newNode;
        p = p.next;
    }
     while( q !== null) {
        let newNode = new ListNode((q.val + jin) % 10);
        jin = Math.floor((q.val + jin) / 10);
        rear.next = newNode;
        rear = newNode;
        q = q.next;
    }
    if(jin !== 0) {
        let newNode = new ListNode(jin);
        rear.next = newNode;
    }
    return rHead.next;
    
};
```
