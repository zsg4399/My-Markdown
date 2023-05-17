## 剑指 Offer 32 - III. 从上到下打印二叉树 III
请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [20,9],
  [15,7]
]


```java
 public List<List<Integer>> levelOrder(TreeNode root) {
      if (root == null) {
                return new ArrayList();
            }
            List<List<Integer>> result = new ArrayList();
            MyQueue<TreeNode> queue = new MyQueue<>(1000);
            List<Integer> list = new ArrayList();
            list.add(root.val);
            queue.add(root);
            HashMap<TreeNode, Integer> map = new HashMap<>();
            map.put(root, 1);
            //高度计数
            int currentHeight = 0;
            TreeNode node;
            while (!queue.isEmpty()) {
                //表明已经到达下一层节点，开始遍历
                node = queue.getHead();
                queue.remove();
                int height = map.get(node);
                if (height != currentHeight) {
                    currentHeight++;
                    if(height%2==0){
                        Collections.reverse(list);
                    }
                    result.add(list);
                    list = new ArrayList<>();
                }
                //当前层采用的栈存储

                if (node.left != null) {
                    queue.add(node.left);
                    list.add(node.left.val);
                    map.put(node.left, height + 1);
                }
                if (node.right != null) {
                    queue.add(node.right);
                    list.add(node.right.val);
                    map.put(node.right, height + 1);
                }

            }
            return result;
    }
```