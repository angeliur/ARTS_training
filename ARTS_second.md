

##### Algorithm

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807



解法：

方法一：自己的解法就是网上给出的暴力法，其他方法就没有想到，还得多练习。



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
            ListNode dummyHead = new ListNode(0);
        ListNode p = l1, q = l2, curr = dummyHead;
        int carry = 0;
        while (p != null || q != null) {
            int x = (p != null) ? p.val : 0;
            int y = (q != null) ? q.val : 0;
            int sum = carry + x + y;
            carry = sum / 10;
            curr.next = new ListNode(sum % 10);
            curr = curr.next;
            if (p != null) p = p.next;
            if (q != null) q = q.next;
        }
        if (carry > 0) {
            curr.next = new ListNode(carry);
        }
        return dummyHead.next;
    
        }
    }

[https://leetcode-cn.com/problems/add-two-numbers/solution/liang-shu-xiang-jia-by-leetcode/](https://leetcode-cn.com/problems/add-two-numbers/solution/liang-shu-xiang-jia-by-leetcode/)





##### Review

[https://developer.android.google.cn/reference/android/support/v7/widget/SnapHelper?hl=en](https://developer.android.google.cn/reference/android/support/v7/widget/SnapHelper?hl=en)

SnapHelper是Android中的RecyclerView控件在24.2.0版本中新增了SnapHelper这个辅助类，用于辅助RecyclerView在滚动结束时将Item对齐到某个位置。例如列表横向，纵向滑动时，很多时候不会让列表滑到任意位置，而是会有一定的规则限制，这时候就可以通过SnapHelper来定义对齐规则了。

SnapHelper是一个抽象类，官方提供了一个LinearSnapHelper的子类，可以让RecyclerView滚动停止时相应的Item停留中间位置。25.1.0版本中官方又提供了一个PagerSnapHelper的子类，可以使RecyclerView像ViewPager一样的效果，一次只能滑一页，而且居中显示



##### Tips

windows用户期盼的Terminal预览版已经上线了，它是微软2019年5月份推出的全新开源终端应用，可以像Mac电脑上的iTerm2和zsh一样，极大地提高程序员的工作效率和使用体验。支持PowerShell、cmd、WSL(Windows的Linux子系统)、SSH等命令行程序。

下载地址：

[https://www.microsoft.com/zh-cn/p/windows-terminal-preview/9n0dx20hk701?activetab=pivot:overviewtab](https://www.microsoft.com/zh-cn/p/windows-terminal-preview/9n0dx20hk701?activetab=pivot:overviewtab)



##### Share

分享一个周末看的电影《死亡诗社》，也许我们每一个曾经的学生和老师都应该都看看，教育的本质到底是什么，我们需要的真的只是能考上大学却没有独立思考能力，并不了解自己真正热爱的事情吗？每个人都应该在学习的过程中形成自己的独立人格和思想，永远充满热情。