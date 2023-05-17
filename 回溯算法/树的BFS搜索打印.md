## 剑指 Offer 32 - II. 从上到下打印二叉树 II

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### Java中没有直接提供队列的数据结构，而是作为部分集合的一个抽象接口,LinkedList可以提供像队列一样的功能，但是占用的比较大，故自己实现了一个队列的数据结构
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class MyQueue<T>{
    class QueueNode<T> {
        T val;
        QueueNode next;
        public QueueNode previos;

        QueueNode(T val) {
            this.val = val;
            next = null;
            previos = null;
        }

        QueueNode() {
        }
    }

    private QueueNode font;
    private QueueNode rear;
    private int size;
    private int maxSize;

    /**
     * Init this Queue
     * DefaultMaxsize=64
     */
    public MyQueue() {
        font = rear = new QueueNode();
        maxSize = 64;
        size = 0;
    }

    /**
     * 手动分配一个队列最大长度
     * @param maxSize
     */
    public MyQueue(int maxSize){
        font = rear = new QueueNode();
        this.maxSize = maxSize;
        size = 0;
    }

    /**
     * 判断队列是否为空
     *
     * @return
     */
    public boolean isEmpty() {
        return size == 0;
    }

    /**
     * 判断队列是否已满
     *
     * @return
     */
    public boolean isFull() {
        return size == maxSize;
    }

    /**
     * 队尾入队
     */
    public boolean add(T val) {
        if (isFull()) {
            return false;
        }
        rear.next = new QueueNode(val);
        rear.next.previos = rear;
        rear=rear.next;
        size++;
        return true;
    }

    /**
     * 队头出队
     *
     * @return
     */
    public boolean remove() {
        if (isEmpty()) {
            return false;
        }
        font.next = font.next.next;
        size--;
        //如果不为空，则让队头节点的后继节点的前继节点指向队头
        if (!isEmpty()) {
            font.next.previos=font;
        }
        
        return true;
    }

    public  T getHead(){
        if(isEmpty()){
            return null;
        }
        return (T)font.next.val;
    }

    public T getLast(){
        if(isEmpty()){
            return null;
        }
        return (T) rear.val;
    }
}

class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
       if(root==null){
           return new ArrayList();
       }
       List<List<Integer>> result=new ArrayList();
       MyQueue<TreeNode> queue=new MyQueue(1000);
       List<Integer> list=new ArrayList();
       list.add(root.val);
       queue.add(root);
       HashMap<TreeNode,Integer> map=new HashMap();
       map.put(root,1);
       int currentHeight=0;
       while(!queue.isEmpty()){
         TreeNode node=queue.getHead();
         Integer height=map.get(node);
         if(height!=currentHeight){
            result.add(list);
            currentHeight++;
            //碰到下一层节点清空list
            list=new ArrayList();
         }
         if(node.left!=null){
             queue.add(node.left);
             map.put(node.left,height.intValue()+1);  
             list.add(node.left.val);   
         }  
         if(node.right!=null){
             queue.add(node.right);
             map.put(node.right,height.intValue()+1);
             list.add(node.right.val);
         }
         //出队
         queue.remove();
       } 
       return result;
    }
}
```