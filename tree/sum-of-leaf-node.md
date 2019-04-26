[Sum of Leaf Node]

* 思路：一般的traverse，判定leaf node的条件为如果左右子树都为空的节点。为了避免设置全剧变量可以设置一个长度为一的数列然后持续更新
* 代码

        <
        public int sumLeafNode(TreeNode root) {
            // Write your code here
            if (root == null) return 0;
            
            int[] sum = new int[]{0};
            helper(root, sum);
            return sum[0];
        }
        
        private void helper(TreeNode root, int[] sum) {
            if (root == null) return;
            
            if (root.left == null && root.right == null) {
                sum[0] += root.val;
                return;
            }
            
            helper(root.left, sum);
            helper(root.right, sum);
        }
        >