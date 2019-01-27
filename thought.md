##leetcode 心得和想法
___

* 以下列表是按照做题顺序，不一定是题号顺序。  
* 编程语言使用java
* and i found this language should use english

___

#### 98. 
这个可以有三种解法:

1. 第一种是按住一个节点，然后检查所有的子节点是不是都满足要求，这样的时间复杂度是 O（n^2^)  
2. 可以通过每次传递上一个节点的大小，检查子节点是否符合要求  
3. 通过递归（暂时还不会）递归代码如下：

```java
 private boolean isIncreasing(TreeNode p){
        if (p == null) return true;
        if (isIncreasing(p.left)){
   			if (prev != null && p.val <= prev.val) return false;
            prev = p;
            return isIncreasing(p.right);
        }
        return false;
    }
```

####104

使用递归的方法，检测出左子树和右子树中最大的一个，然后加一，即为这一层的最大深度

####111
as for the MinDepth of Binary Tree, we have to make sure the depth do mean the root to the _leaf node_ and this means there are no child, 如果有一个child，左子树或者右子树的节点不叫_child(leaf)_ 

* 这种是dfs（deep－first－search)

```java
 public int minDepth(TreeNode root) {
 	//当root ＝＝ null时，不意味着这个点是leaf，而是这个点就不存在，是相当于leaf的两个子节点之一
        if (root == null) 
            return 0;
        if (root.left == null)
            return minDepth(root.right)+1;
        if (root.right == null)
            return minDepth(root.left)+1;
            //这里算min的时候一定要记得＋1 是在min后边的（括号问题）
        return Math.min(minDepth(root.left), minDepth(root.right)+1);
    }
    
``` 

* 这种是bfs（Deep——first－search）

```java
   if (root == null) return 0;
        
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        TreeNode rightMost = root;
        int depth = 1;
        while(!q.isEmpty()){
        ／／开始进行层遍历，从左到右，直到最右的节点，通过queue的数据结构
            TreeNode node = q.poll();
            if(node.left == null && node.right == null) break;
            if(node.left != null) q.add(node.left);
            if (node.right != null) q.add(node.right);
            
            if(node == rightMost){
                depth ++;
                rightMost = (node.right == null) ? node.left: node.right;
            }
        }
        return depth;
    }
```

####110
寻找是否为平衡二叉树，在这道题当中的brute force解法，不仅仅要求左右子树的深度差不超过1，还要检查左右子树是否平衡，否则会出现很奇怪的现象，左右的深度相同，却不平衡的状态。

```java
  public boolean isBalanced(TreeNode root) {
        if (root == null) return true;
        return Math.abs(maxDepth(root.left)-maxDepth(root.right)) <= 1
            &&isBalanced (root.left)
            && isBalanced(root.right);
            
    }
    public int maxDepth(TreeNode root){
        if (root == null) 
            return 0;
        return Math.max(maxDepth(root.left),maxDepth(root.right))+1;
    }
    ```

