1.在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

### 数组

```cpp
class Solution {
public:
    bool Find(int target, vector<vector<int> > array) {
        int col = array[0].size();
        int row = array.size();
        int i,j;   // i为列 j为行
        for(i = col-1,j=0; i>=0 && j<row;){
            if(target == array[j][i]){
                return true;
            }
            if(target < array[j][i]){   //如果目标值比右上角小，则左移
                i--;
                continue;
            }
            if(target > array[j][i]){    //如果目标值比右上角大，则下移
                j++;
                continue;
            }
        }
        return false;
    }
};
```

2.请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

### 字符串

```cpp
class Solution {
public:
    void replaceSpace(char *str,int length) {
        if(str==NULL||length<0)
            return ;
        int oldLength =0,spaceLength =0, i=0;
        while(str[i] != '\0'){
            oldLength +=1;
            if(str[i]== ' '){
                spaceLength+=1;
            }
            i++;
        }
        //计算空间长度
        int newLength = oldLength + 2 * spaceLength;
          if(newLength>length)
            return ;
        while(oldLength >= 0 && newLength > oldLength){
            if(str[oldLength] == ' '){
                str[newLength--] = '0';
                str[newLength--] = '2';
                str[newLength--] ='%';
            }else{
                str[newLength--] = str[oldLength];
            }
            oldLength--;
        }

    }
};
```

3.输入一个链表，从尾到头打印链表每个节点的值。

### 链表

```java
/**
*    public class ListNode {
*        int val;
*        ListNode next = null;
*
*        ListNode(int val) {
*            this.val = val;
*        }
*    }
*
*/
import java.util.Stack;
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        Stack<Integer> stack = new Stack<>();
        ListNode l = listNode;
        ArrayList<Integer> a = new ArrayList<>();
        while(l != null){
            stack.push(l.val);   // 入栈，将值从数组压入栈
            l = l.next;
        }
        while(!stack.empty()){
           a.add(stack.pop());   // 出栈，将值存入数组
        }
        return a;
    }
}
```

4.输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

### 树

```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        TreeNode root = reConstructTree(pre,0,pre.length-1,in,0,in.length-1);
        return root;
    }
    public TreeNode reConstructTree(int [] pre,int startPre,int endPre,int [] in,int startIn,int endIn){
        if(startPre>endPre||startIn>endIn)
            return null;
        TreeNode root = new TreeNode(pre[startPre]);
        for(int i = startIn;i<=endIn;i++)
            if(pre[startPre] == in[i]){  //在中序遍历中找到根结点
            root.left = reConstructTree(pre, startPre+1, startPre+i-startIn, in, startIn, i-1); //左子树
            root.right = reConstructTree(pre,startPre+i-startIn+1,endPre,in,i+1,endIn);  //右子树
            break;
            }
        return root;
    }
}
```

思路：找出前序遍历序列的左右子树，中序遍历序列的左右子树，总共4个数组，然后递归调用。思路：找出前序遍历序列的左右子树，中序遍历序列的左右子树，总共4个数组，然后递归调用。

![](/assets/8788852_1496674193455_D60F8B66AA5C0250BB4D8DDD6DD73335.png)

5.用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

### 栈和队列

思路：stack1作为入队列 ，stack2作为出队列，实现先进先出

```java
import java.util.Stack;

public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();

    public void push(int node) {
        stack1.push(node);
    }

    public int pop() {
        int n ;
        if(stack2.empty()){   //如果stack2为空，则stack1的都倒入stack2
            while(!stack1.empty()){
            n = stack1.pop();   //从1出栈，倒入2
            stack2.push(n);
            }           
        }
        //如果不为空，stack2直接出栈
        n = stack2.pop();
        return n;
    }
}
```



