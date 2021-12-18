```javascript
public class SolutionTwoSum {

    public static void main(String[] args) {
        ListNode randomListNode1 = generateRandomListNode(5);
        printListNode(randomListNode1);
        ListNode randomListNode2 = generateRandomListNode(4);
        printListNode(randomListNode2);
        ListNode listNode = addTwoNumbers(randomListNode1, randomListNode2);
        printListNode(listNode);
    }

    /**
     * 两个整数以单向链表的形式倒序相加
     *
     * @param l1 ListNode
     * @param l2 ListNode
     * @return ListNode
     */
    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        // 以一个头节点开始，初始化链表，并赋值给 resultNode
        ListNode headNode = new ListNode();
        ListNode resultNode = headNode;
        // 余数
        int remainder;
        // 进位
        int carry = 0;

        // 被迭代的操作：
        // 1. 求两个节点值与进位的和
        // 2. 余数放在当前节点（新节点），进位保留到下一次遍历或完成迭代时使用
        // 3. resultNode 的链表新增节点，并用 headNode 作为指针移动，准备下一次迭代
        while (l1 != null || l2 != null) {
            int tmpVal1 = l1 != null ? l1.val : 0;
            int tmpVal2 = l2 != null ? l2.val : 0;
            int sum = tmpVal1 + tmpVal2 + carry;

            remainder = sum % 10;
            carry = sum / 10;

            headNode.next = new ListNode(remainder);
            headNode = headNode.next;

            l1 = l1 != null ? l1.next : null;
            l2 = l2 != null ? l2.next : null;
        }

        // 当两个节点都遍历结束时，需考虑最后一次操作是否有进位
        if (carry > 0) {
            headNode.next = new ListNode(carry);
        }

        return resultNode.next;
    }

    /**
     * 生成固定长度的，节点值随机的单向链表
     *
     * @param length 需要的链表长度
     * @return 生成的单向链表
     */
    public static ListNode generateRandomListNode(int length) {
        if (length < 1) {
            return null;
        }
        ListNode headNode = new ListNode();

        ListNode resultNode = headNode;

        for (int i = 0; i < length; i++) {
            int randomNum = (int) (Math.random() * 10);
            headNode.next = new ListNode(randomNum);
            headNode = headNode.next;
        }

        return resultNode.next;
    }

    /**
     * 打印单向链表
     *
     * @param node 单向链表
     */
    public static void printListNode(ListNode node) {
        String concatSymbol = "-";
        while (node != null) {
            if (node.next == null) {
                System.out.println(node.val);
                break;
            }
            System.out.print(node.val + concatSymbol);
            node = node.next;
        }
    }

}

class ListNode {
    int val;
    ListNode next;

    ListNode() {
    }

    ListNode(int val) {
        this.val = val;
    }

    ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }
}

```
