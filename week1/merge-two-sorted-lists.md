## 题目地址
[21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

## 解题
这里新开一个链表用来存储合并后的结果。由于需要返回这个链表，所以设置一个head节点用于记录链表的开始，并且由于需要一直往后追加元素，所以这个链表需要新增加一个指针pointer=head。
<br>遍历list1和list2两个链表，判断头节点哪个最小，头节点小的追加到pointer后，并且该链表节点向后移一位，继续和另一个链表的头节点比较，以此类推。
<br>另外，循环的判断条件是list1 != null && list2 != null，任意链表满足即终止循环，假设只有某一个链表到头了，另一个链表还会有元素剩余，因此需要追加到结果链表的末尾。

## 时空复杂度分析
由于需要从头到尾遍历完两个链表，因此时间复杂度为O(m+n)。
<br>
最终返回的新链表长度一定是m+n，因此空间复杂度是O(m+n)。

## 代码
```Java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode head = new ListNode();
        ListNode pointer = head;
        // 这里不用list1.next != null否则最后会剩下一个元素无法被追加
        while (list1 != null && list2 != null) {
            if (list1.val <= list2.val) {
                pointer.next = list1;
                list1 = list1.next;
            } else {
                pointer.next = list2;
                list2 = list2.next;
                
            }
            pointer = pointer.next;
        }
        // 如果其中一个链表还有没处理完的值，需要追加到结果末尾
        if (list1 == null) {
            pointer.next = list2;
        } else {
            pointer.next = list1;
        }
        return head.next;
    }
}
```
