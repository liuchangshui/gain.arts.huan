# ARTS WEEK01 (0415-0421)
## Algorithm 
### 题目
```
2. Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:
	Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
	Output: 7 -> 0 -> 8
	Explanation: 342 + 465 = 807.
	
```

### 解法 1
```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //设置初始节点对象
        ListNode listnode = new ListNode(0);
        //设置临时节点
        ListNode tempNode = listnode;
        int offsetNodeNum = 0;
        
        while (l1 != null || l2 != null){
            //取listNode对象中的第一个值
            int num1 = l1 == null ? 0 : l1.val;
            int num2 = l2 == null ? 0 : l2.val;
            //节点值+进位标识 求和
            int sum = num1 + num2 + offsetNodeNum;
            //判断和值是否大于等于10,若大于等于10,则进位标识设置为1
            offsetNodeNum = sum >= 10 ? 1 : 0;
            tempNode.next = new ListNode(sum % 10);
            tempNode = tempNode.next;
            if(l1 != null){l1 = l1.next;}
            if(l2 != null){l2 = l2.next;}
        }
        
        if(offsetNodeNum == 1){
            tempNode.next = new ListNode(1);
        }
        
        return listnode.next;
    }
}

```