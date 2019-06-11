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

另一种解法是通过递归，然后当发现不平衡的子树的时候，直接返回－1， 然后依次递归返回，这样才能做到o（n）

```java
 public boolean isBalanced(TreeNode root) {
//         this means if the maxdepth of this node is -1 ,return 0, means unbalanced
//         which is -1 means unbalanced, other value mean balance;
        return maxDepth(root) != -1;
        
    }
    
    private int maxDepth(TreeNode root){
//         leaf 
//要注意空指针异常，这里是因为root可能会是null ，我们必须先吧null的情况说明怎们办（return 0）
        if (root == null) return 0;
        
        int l = maxDepth(root.left);
        int r = maxDepth (root.right);
//         this subtree is unbalanced
        if (l == -1)
            return -1;
        if (r == -1)
            return -1;
//         return the maxdepth of l or r /is unbalanced return -1
        return (Math.abs(l - r) <= 1) ? (Math.max(l,r) + 1) : -1;
    }
```

#### 108

这道题和二叉搜索很像，递归的放置每一个跟节点，然后是左子树和右子树，（假想叶子节点后其实还跟着两个null，就容易解释了，这个观点感觉和linked list中null头一样）

```java
    public TreeNode sortedArrayToBST(int[] nums) {
        return sortedArrayToBST(nums,0,nums.length -1);
    }
    
    private TreeNode sortedArrayToBST(int[] arr, int start, int end){
        if (start > end ) return null;
        int mid = (start + end)/2;
        TreeNode node = new TreeNode(arr[mid]);
//         because the mid is already placed
        node.left = sortedArrayToBST(arr,start, mid - 1);
        node.right = sortedArrayToBST(arr, mid + 1, end);
        return node;
    }
```


#### 109 
1. 简单办法就是强行搞，把链表当作数组，访问费时间
2. 复杂办法就是从地下往上走（bottom－up） ，可以理解为中序遍历（？那为什么不能是pre－order or  post-order)???
 有可能是因为二分法排序后产生的数列就是按照中序遍历出来的，所以为了反相做，不得不使用中序遍历。
 
####124

如果子树为negetive，那么我们就不考虑他，因为他不会给我们带来add number，然后maxSum 就直接等于 p.value ＋ left ＋right,  然后取最大值，因为如果产生－的数据已经被忽略成为了0；
但是这就引发了recursive 的函数return的是子树的数据大小，而不是maxSum，这也导致了必须有另一个变量纪录maxVal，这使用一个private （局部）全局变量

####136.
1. 用map，此时相同的key会被覆盖

	```java
	  public int singleNumber(int[] nums) {
//           key  ,value
        Map <Integer, Integer> map = new HashMap<>();
        for (int x : nums){
//             if ehere is a value in the map, get the value of it
            int count = map.containsKey(x) ? map.get(x): 0;
//             if key is same ,the value will be overwrited
            map.put(x , count +1);
            System.out.println(x);
        }
        for (int x : nums){
            if(map.get(x) == 1){
                return x;
            }
        }
         throw new IllegalArgumentException("No single element");    
    }
    ```
2. 使用set

iterator是什么

#### 54
这道题告诉我们 ＋＋i比i++好用

####13 
map的初始化的另一种方式

```java
private Map<Character, Integer> map =      new HashMap<Character, Integer>() {{            put('I', 1);  put('V', 5);   put('X', 10);            put('L', 50); put('C', 100); put('D', 500);            put('M', 1000);}};
```
#### 334
使用动态规划先吧min，max求出来，最后检查在特定范围内，有没有满足的数，

``` java
public boolean increasingTriplet(int[] nums) {
    
    
    int len = nums.length;
    if(len < 3)
        return false;
    int[] min = new int[len]; 
    int[] max = new int[len]; 
    
    min[0] = nums[0];
    for(int i = 1; i < len; i++){      
        min[i] = Math.min(min[i-1],nums[i]);
    }
    max[len-1] = nums[len-1];
    for(int i = len-2; i>=0; i--){
        max[i] = Math.max(max[i+1],nums[i]);
    }
    
    for(int i = 0; i < len; i++){
        if(max[i] > nums[i] && nums[i] > min[i])
            return true;
    }
    return false;
}
```

第二种解法

``` java
public boolean increasingTriplet(int[] nums) {
        if (nums.length < 3) {
            return false;
        }
        int i, j, k;
        i = nums[0];
        j = Integer.MAX_VALUE;
        k = Integer.MAX_VALUE;

        for (int l = 0; l < nums.length; l++) {
           //update the i
           //如果存在更小的，需要更新i
           if (nums[l] < i) {
                i = nums[l];
            }
            
            //get the j
            //问题会发生，主要是更新j的值
            //nums[l]>i 是为了保证他是第二小，num[l] < j 是为了保证如果有更第二小的存在，可以及时更新
            if(nums[l] > i && nums[l] < j){
                j= nums[l];
            }
            
            //    if the k is available return true
            if(nums[l]> j){
                return true;
            }
        }
        return false;
    }
```
    