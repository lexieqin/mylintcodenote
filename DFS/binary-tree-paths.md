[Binary Tree Path]

* 思路：一般的DFS思路，跳出递归的条件为走到叶子节点
* 代码

        <
        public List<String> binaryTreePaths(TreeNode root) {
            // write your code here
            List<String> paths = new ArrayList<>();
            if (root == null) return paths;
            String path = "";
            helper(paths, path, root);
            return paths;
        }
        
        private void helper(List<String> paths, String path, TreeNode node) {
            if (node == null) return;
            if (node.left == null && node.right == null) {
                path += node.val;
                // System.out.println(path);
                paths.add(new String(path));
                return;
            }
            path += node.val + "->";
            helper(paths, path, node.left);
            helper(paths, path, node.right);
        }
        >