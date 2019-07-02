- 思路： 递归的时候把max的值作为数组传进去，helper func每次返回最大的root to leaf值
- 代码

        public int maxPathSum(TreeNode root) {
            // write your code here
            if (root == null) return 0;
            int[] max = new int[]{Integer.MIN_VALUE};
            helper(root, max);
            return max[0];
        }
        
        private int helper(TreeNode root, int[] max) {
            if (root == null) return 0;
            int left = Math.max(helper(root.left, max), 0);
            int right = Math.max(helper(root.right, max), 0);
            max[0] = Math.max(left + root.val + right, max[0]);
            return Math.max(left, right) + root.val;
        }