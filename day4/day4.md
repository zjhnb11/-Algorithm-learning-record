# day4

## 24. Swap Nodes in Pairs

有时候对题目理解会有误差，比如这次的理解就会认为是相邻两个节点交换，而不是1 and 2，3 and 4交换。

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummyhead = new ListNode();//也可以不传入‘-1’
        dummyhead.next = head;//这里不能忘记.next。要严格按照笔记来写
        ListNode cur = dummyhead;
        ListNode temp = null;
        ListNode temp1 = null;
        while(cur.next != null &&  cur.next.next!=null){
            temp = cur.next;
            temp1 = cur.next.next.next;
            cur.next = cur.next.next;
            cur.next.next = temp;
            temp.next = temp1;
            cur = cur.next.next;
        }
        return dummyhead.next;


    }
}
```

## 19. Remove Nth Node From End of List

想不通的难点:

1.找到倒数的第n个节点。
其他都好说

carl视频解决的方案：
快慢指针法。
根据快慢指针的间隔n，让快指针指向null的时候，慢指针自然的指向了所需的节点

步骤1：先拉开快慢指针的间距。
步骤2：然后将两个指针向后迭代，直到fast指针指向null

```
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummyhead = new ListNode();
        dummyhead.next = head;
        ListNode fast = dummyhead;
        ListNode slow = dummyhead;

        for(int i =0;i<=n;i++){
            fast = fast.next;
        }

        while (fast.next != null){
        fast = fast.next;
        slow = slow.next;
    }

    slow.next = slow.next.next;
    return dummyhead.next;
    }
}
```

## 160. Intersection of Two Linked Lists

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode curA = headA;
        ListNode curB = headB;
        int lenA = 0, lenB = 0;
        while (curA != null) { // 求链表A的长度
            lenA++;
            curA = curA.next;
        }
        while (curB != null) { // 求链表B的长度
            lenB++;
            curB = curB.next;
        }
        curA = headA;
        curB = headB;
        // 让curA为最长链表的头，lenA为其长度
        if (lenB > lenA) {
            //1. swap (lenA, lenB);
            int tmpLen = lenA;
            lenA = lenB;
            lenB = tmpLen;
            //2. swap (curA, curB);
            ListNode tmpNode = curA;
            curA = curB;
            curB = tmpNode;
        }
        // 求长度差
        int gap = lenA - lenB;
        // 让curA和curB在同一起点上（末尾位置对齐）
        while (gap-- > 0) {
            curA = curA.next;
        }
        // 遍历curA 和 curB，遇到相同则直接返回
        while (curA != null) {
            if (curA == curB) {
                return curA;
            }
            curA = curA.next;
            curB = curB.next;
        }
        return null;
    }
}
```

## 142. Linked List Cycle II

难点在于如何解决数学问题

数学证明后代码就很简单

```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {// 有环
                ListNode index1 = fast;
                ListNode index2 = head;
                // 两个指针，从头结点和相遇结点，各走一步，直到相遇，相遇点即为环入口
                while (index1 != index2) {
                    index1 = index1.next;
                    index2 = index2.next;
                }
                return index1;
            }
        }
        return null;
    }
}
```

