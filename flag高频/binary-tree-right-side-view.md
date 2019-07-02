[Binary Tree Right Side View]
- 思路: level order traverse
- 代码

        public List<Integer> rightSideView(TreeNode root) {
            // level order traverse 
            List<Integer> view = new ArrayList<>();
            if (root == null) return view;
            Queue<TreeNode> queue = new LinkedList<>();
            queue.offer(root);
            while (!queue.isEmpty()) {
                view.add(queue.peek().val);
                int size = queue.size();
                for (int i = 0; i < size; i++) {
                    TreeNode curr = queue.poll();
                    if (curr.right != null) {
                        queue.offer(curr.right);
                    }
                    if (curr.left != null) {
                        queue.offer(curr.left);
                    }
                }
            }
            return view;
        }