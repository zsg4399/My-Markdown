### 剑指 Offer 32 - I. 从上到下打印二叉树

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回：

[3,9,20,15,7]

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 解法，用队列来做
```java
public int[] levelOrder(TreeNode root) {
      List<Integer> result=new ArrayList();
      //BFS搜索需要用到队列结构,Linkedlist实现了DQueue接口，可以当做双向队列来使用
      LinkedList<TreeNode> list=new LinkedList();
      if(root!=null){
      result.add(root.val);
      //加入队列
      list.add(root);
      }
      while(!list.isEmpty()){
        //获取队头节点
        TreeNode node=list.getFirst();
        if(node.left!=null){
            result.add(node.left.val);
            //加入队尾
            list.addLast(node.left);
        }
    
        if(node.right!=null){
            result.add(node.right.val);
            //加入队尾
            list.addLast(node.right);
        }
        //队头出队
        list.removeFirst();
      }
      return result.stream().mapToInt(Integer::intValue).toArray();
    }
```