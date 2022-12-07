## 题目地址
[66. 加一](https://leetcode.cn/problems/plus-one/)

## 解题
这题比较难处理的就是进位问题，本题因为只涉及+1，因此会产生进位的只是值为9的位置。其他位置直接+1即可。
直接从最后一位开始遍历，如果是9的话就设置为0，并继续往前，找到不是9的那一位+1。
如果全部都是9的话，说明要想完成进位当前数组长度是不够的，实际长度要比当前大一位，因此重新分配一个length+1的数组空间，并且把第一位赋值为1，其余位是默认值0。

## 时空复杂度分析
只需从头到尾遍历一次数组即可完成，因此时间复杂度是O(n)。
当发生进位时导致数组长度不够使用时，涉及重新申请数组空间，并且空间大小为n+1，因此空间复杂度为O(n).

## 代码
```java
class Solution {
    public int[] plusOne(int[] digits) {
        for (int i = digits.length - 1; i >= 0; i--) {
            if (digits[i] == 9) {
                if (i == 0) {
                    int[] ans = new int[digits.length + 1];
                    ans[0] = 1;
                    return ans;
                } else {
                    digits[i] = 0;
                    continue;
                }
            } else {
                digits[i] += 1;
                break;
            }
        }
        return digits;
    }
}
```
