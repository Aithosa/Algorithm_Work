## 题目地址
[641. 设计循环双端队列](https://leetcode.cn/problems/design-circular-deque/)

## 解题
这里用双向链表来模拟，需要特别注意的是从前端和后端插入和删除元素这四个方法。
<br>对于插入元素，插入时要判断当前队列是不是为空，如果不是要维护好队首和队尾的链表关系。
<br>对于删除元素，删除时要特别判断删除完之后队列是不是为空，如果是在队首删除，删除完如果没有元素了，需要把head和tail同时赋值为null(不然即使队列删空head和tail也会有值)。

## 时空复杂度分析


## 代码
```java
class MyCircularDeque {
    /**
     * 双向链表
     */
    private static class DoubleLinkNode {
        int val;

        DoubleLinkNode prev;

        DoubleLinkNode next;

        DoubleLinkNode(int val) {
            this.val = val;
        }
    }

    /**
     * 最大容量
     */
    private int capacity;

    /**
     * 当前容量
     */
    private int size;

    /**
     * 头指针
     */
    private DoubleLinkNode head;

    /**
     * 尾指针
     */
    private DoubleLinkNode tail;

    /**
     * 有参构造函数
     */
    public MyCircularDeque(int k) {
        capacity = k;
        size = 0;
    }

    /**
     * 无参构造函数
     */
    public MyCircularDeque() {}

    /**
     * 从前侧插入元素
     */
    public boolean insertFront(int value) {
        if (size == capacity) {
            return false;
        }
        DoubleLinkNode node = new DoubleLinkNode(value);
        if (size == 0) {
            head = node;
            tail = node;
        } else {
            node.next = head;
            head.prev = node;
            head = node;
        }
        size++;
        return true;
    }

    /**
     * 从后侧插入元素
     */
    public boolean insertLast(int value) {
        if (size == capacity) {
            return false;
        }
        DoubleLinkNode node = new DoubleLinkNode(value);
        if (size == 0) {
            head = node;
            tail = node;
        } else {
            tail.next = node;
            node.prev = tail;
            tail = node;
        }
        size++;
        return true;
    }

    /**
     * 从前侧删除元素
     */
    public boolean deleteFront() {
        if (size == 0) {
            return false;
        }
        head = head.next;
        if (head != null) {
            head.prev = null;
        } else {
            // 此时head已经为null，队列为空，把tail也赋值为null
            tail = null;
        }
        size--;
        return true;
    }

    /**
     * 从后侧删除元素
     */
    public boolean deleteLast() {
        if (size == 0) {
            return false;
        }
        tail = tail.prev;
        if (tail != null) {
            tail.next = null;
        } else {
            // 此时tail已经为null，队列为空，把head也赋值为null
            head = null;
        }
        size--;
        return true;
    }

    /**
     * 返回队首元素
     */
    public int getFront() {
        if (size == 0) {
            return -1;
        }
        return head.val;
    }

    /**
     * 返回队尾元素
     */
    public int getRear() {
        if (size == 0) {
            return -1;
        }
        return tail.val;
    }

    /**
     *队列是否为空
     */
    public boolean isEmpty() {
        return size == 0;
    }

    /**
     *队列是否满
     */
    public boolean isFull() {
        return size == capacity;
    }
}
```
